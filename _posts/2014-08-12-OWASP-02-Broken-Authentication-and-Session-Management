---
layout: post
title: OWASP 02 - Broken Authentication and Session Management
date: 2014-08-12
---

Continuing the series on the OWASP top ten vulnerabilities, we now turn our attention to the second item, [Broken Authentication and Session Management](https://www.owasp.org/index.php/Top_10_2013-A2-Broken_Authentication_and_Session_Management).

There are many, varied risks that are opened up by having badly implemented authentication or sessions. It takes a little more consideration to figure out exactly what the risks are when compared to the graphic directness of a SQL injection attack, it boils down to one simple thing:

Your application may allow an attacker to impersonate a legitimate user. That user might be a customer, someone who has trusted you with their information. That would be bad. That user might be an administrator, or even you, the developer. That would be all kinds of bad. All at once.

Demonstration, part the first
=============================

Let's look again at [Mr. Hunt's security sandbox site](http://hackyourselffirst.troyhunt.com/). We'll start off by registering an account.

Hmm. No SSL. So we're about to send our new username and password over an unencrypted connection. Really we could stop there, that's bad enough. But let's dig a little deeper. Choose a username and password (no longer than ten characters, if you don't mind).

Cookies are a likely candidate for leaking information that shouldn't be leaked. There's an `AuthCookie` in there, which expires at the end of this session, so when we close the browser it's gone. I'm lazy, and I don't like typing passwords. Log out and back in again, but this time choose "Remember me".

That's better, now we have a login that's valid for a whole year. (We'll come back to that later). But wait, what's this?

There's a `password` cookie. For some reason, the site wants my browser to remember that. Fortunately the password itself is obscured by some indecipherable cipher:

	Password=cGFzczEyMzQ=;

Back to the command line:

	~$ echo cGFzczEyMzQ= | base64 -d
	pass1234

Okay, maybe not so indecipherable after all. Better log out!

Only after logging out, the cookie is still there, along with it's buddy...

	Email=terry@example.com

Email and password, both just waiting for whoever uses this computer after us. Your users never reuse passwords, right?

Demonstration, part the second
==============================

Okay, that example was a little extreme. I've never seen anything quite so bad in practice (but I'm sure it's out there). There other, more insidious issues at play here.

Remember that `AuthCookie`, the one that we got for a year? Make a copy of that, then log out. Then try something like this...

	~$ curl -b "AuthCookie=E234...B5F" hackyourselffirst.troyhunt.com

	...lots of stuff...
	<li><a>Hello Terry!</a></li>

Yup. That cookie still works. All that the logout function did was delete it from the client side.

Now seeing as the cookie was previously sent in unencrypted HTTP, it wouldn't take all the hacking power of the NSA to snoop it. Heck, some kid with a [pineapple](https://hakshop.myshopify.com/products/wifi-pineapple) could have stolen it. And that cookie counts as a valid login for a whole year.

Mitigation
==========

This is one where you really have to be proactive in finding out if you have a problem. As an attacker can spoof a real user, it might not be obvious when an attack does occur.

If at all possible, don't handle authentication at all. If you can, use a robust solution like [OAuth](http://oauth.net/2/) and follow the implementation steps to the letter.

Failing that, there are a few really simple steps to take to minimize the possible attacks:

 * Be very hesitant to weaken login requirements (through "password hints" and other ill-advised recovery mechanisms). When you can, strengthen them (by using two factor auth, for example).
 * Don't expose login credentials or tickets by using plain HTTP.
 * Timeout your sessions / auth tokens, and kill them when the user logs out.
 * Protect your backend as well. Hash all your user's passwords. And hash them strongly. This is 2014, a desktop machine can compute [literally billions of MD5 or SHA1 hashes *per second*](http://blog.codinghorror.com/speed-hashing/).

This certainly isn't everything. Investigate the references on the OWASP page, particularly the "cheat sheets" to get up to speed fast.
