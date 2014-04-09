---
layout: post
title: Developer tools for mobile
date: 2014-04-09
---

I've been doing a fair bit of mobile development recently. One of the little niggles that makes life more difficult is the lack of a HTML / JavaScript / CSS inspector on mobile devices. Coming to the rescue, Google has been quietly adding several features to Chrome that are making life easier for developers targeting mobile.

[Mobile emulation](https://developers.google.com/chrome-developer-tools/docs/mobile-emulation) makes the desktop browser behave more like a mobile device. This little tab tucked into the bottom panel of the developer tools can make Chrome take on the screen size, user agent and other features of a mobile device, and also simulate touch events, device orientation etc.

While mobile emulation is a great boost to quickly testing mobile pages, you still sometimes want to use a real device. This is where [remote debugging](https://developers.google.com/chrome-developer-tools/docs/remote-debugging) comes in handy. Using ADB, Chrome can connect to an Android device and provide many of the desktop developer tools to debug a page open in the Android browser.

Finally, it's worth mentioning solutions for when Chrome can't be used, such as when developing a non-browser HTML application (such as a PhoneGap / Cordova app), or deploying to a different mobile platform. I've had some success with [Weinre](https://github.com/apache/cordova-weinre), which is made by Apache as part of the Cordova project. Weinre provides an interface to allow visual debugging of anything that runs HTML/JS. It's a bit fiddly to set up compared to the other options, but incredibly impressive to see in action.

All of the above three options take a lot of the guesswork out of developing layouts and scripts for mobile devices.
