---
layout: post
title: Quick hint - Google Static Maps API
date: 2014-05-28
---

In a web application it's fairly common to use a map to show your user a location, area, travel route etc. 

More often than not, you'll use the Google Maps JavaScript API to do this.
Sometimes this API feels a little more heavy than is really required.
For example, I've wanted to just show a single pushpin on a thumbnail sized map to give users an idea of where a report came from, no interactivity needed.

Today, while working on something along those lines
(popping up a little map to confirm that a GPS location was entered correctly),
I came across [Google's "static maps" API](https://developers.google.com/maps/documentation/staticmaps/index). Not sure how long this has been around, but it's already in version two.

Using the static maps service, it took around ten minutes to get a little map popup. Not bad at all.

![Static maps API example](https://maps.googleapis.com/maps/api/staticmap?center=Brooklyn+Bridge,New+York,NY&zoom=13&size=600x300&maptype=roadmap&markers=color:blue%7Clabel:S%7C40.702147,-74.015794&markers=color:green%7Clabel:G%7C40.711614,-74.012318&markers=color:red%7Clabel:C%7C40.718217,-73.998284&sensor=false)

This image right here is generated from the API!
