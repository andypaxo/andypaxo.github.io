---
layout: post
title: OWASP 04 - Insecure direct object references
date: 2014-10-25
---

Number four in our run through of the OWASP greatest hits is "[Insecure direct object references](https://www.owasp.org/index.php/Top_10_2013-A4-Insecure_Direct_Object_References)". Although the name may not be immediately familiar, the concept is simple indeed.

This is what some refer to as "URL hacking". Simply find a link to a resource restricted to only you `/secret_things?id=123`, and play around with it a bit. In most cases this will harmlessly lead to a 403 or a 404, but in some cases `/secret_things?id=111` will lead to *someone else's secret things*.

Demonstration
===

I've knocked together a simple site to show off this problem and demonstrate how easily it can creep in. Have a look at [potionbook.herokuapp.com](http://potionbook.herokuapp.com), a handy little utility that lets you organize your accumulated alchemical knowledge. (Which, I'm sure, everybody has an urgent need to do).

![Picture of site acting normally](/assets/owasp04-potionbook-normal.png)

Log on to the site and play about for a minute, I'll wait.

Okay! If you've been paying attention so far, you'll have noticed a suspicious looking URL&hellip; something along the lines of `/editpotion/123`.

Try tweaking with that URL, change the number and try again. Lo and behold, you're looking at someone else's data (probably mine). You'll find that because the POST is secured in the same way as the GET (i.e. not at all), you can also modify the data on the resulting page and save it.

Prevention
===

This kind of thing is a simple error of omission. If you look at the [source for this project](https://github.com/andypaxo/potionbook), you'll notice that whilst the listing page only retrieves items for the current user, the edit page does not check if the item it is retrieving is actually owned by said user.

OWASP recommends two ways of dealing with this problem.

The first is to not use direct references to the item in the database (notice how, on our example site, the ID in the URL is literally the primary key in the database). Instead, you can make indirect references that are generated just for the logged in user or their session and do not work outside of that context. For example, a link that expresses "The third item created by this user", rather than "the item with ID 345". This can work when building a new system, but is rather hard to retrofit into an existing application.

The second, most obvious, way is to simply check that the object being requested is actually viewable by the user requesting it. You have to take care here that *every* request checks for access, and does it correctly. In the example application, the code does check that a user is logged in, but doesn't check if it's the *right* user. This can get complicated in the case of systems with complex access controls.

There is an approach that seems to occur to some developers which doesn't fix the problem. If you're thinking "well, those integer IDs are guessable, so I'll just switch to GUID IDs, then the problem of guessing URLs is fixed", then you're only solving half the problem. Remember that URLs can be bookmarked, shared, emailed and indexed by search engines. It's true that GUIDs (when properly generated) are not guessable, but if those identifiers are leaked in any way, you *still* need to have proper access controls.