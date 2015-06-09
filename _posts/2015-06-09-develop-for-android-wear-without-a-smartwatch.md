---
layout: post
title: Developing for Android Wear without a smart watch
date: 2015-06-09
---

Getting started with a new hardware technology always presents a bit of a catch-22 situation. You want to use the technology that you're developing for, but you don't really want to commit to buying one until you've tried developing for it. I'm going to try and do some Android Wear development without actually having a smart watch to begin with (I'm holding out for the successor to the Moto 360, which is likely to come out later this year).

With Android, it's always been possible to develop against an emulator. What makes Wear a little more tricky is that it really requires *two* devices, as the vast majority of Wear apps are bundled extras that come with an Android phone/tablet app.

I'm going to be using Android Studio exclusively for Wear development. Eclipse is familiar and cosy, but going forward, it seems that Google is dropping support and moving 100% to Android Studio. (Which, to anyone who has used IntelliJ or any other JetBrains product, won't feel *too* unfamiliar). Using Studio gives us the option of starting a new project with Wear support already built in. Nice!

After installing an emulator for the watch, the functionality in the template app works fine. But that's not enough! We want to see the phone app send notifications to the watch app. We can do that by pairing a physical android phone to an emulated watch.

There are very comprehensive instructions on how to pair the real phone to the fake watch on the [Android developers site](https://developer.android.com/training/wearables/apps/creating.html), but in brief - you just need to do this:

1. Deploy the app you want to test to both devices
1. Install the [Android Wear app](https://play.google.com/store/apps/details?id=com.google.android.wearable.app) on your phone
1. Connect the phone to the emulator using `adb` like this:

	```adb -d forward tcp:5601 tcp:5601```
	
4. Pair it with the emulator. You can do this by tapping the menu in the top right when pairing. (And, of course, enable notifications)

	![Wear pairing](/assets/20150609/pair wear.png)

And, boom! Things just work.

![Wear notification](/assets/20150609/phone2wear.png)