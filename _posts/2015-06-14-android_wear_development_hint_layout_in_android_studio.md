---
layout: post
title: Android Wear development hint - Layout in Android Studio
date: 2015-06-14
---

I had a bit of an issue when first starting an Android Studio project for wearables. The initial setup went really smoothly, File > New Project > Click to win. However the next bit isn't so great. Click on the layout xml file and instead of seeing the generated default activity layout, you see this:

![android studio layout error](/assets/20150614/android studio layout error.PNG)

"This version of the rendering library is more recent than your version of Android Studio. Please update Android Studio". So of course, the first thing you try is to update Android Studio. And, of course, there are no updates available.

To quickly fix this, you can just change the Android version from 22 MNC to a lower version, like this:

![android studio layout fixed](/assets/20150614/android studio layout fixed.PNG)

Unfortunately, you'll need to make the switch every time you open a layout. To **keep** this setting set correctly, you also need to *uncheck* "Automatically pick best". (Apparently the "best" version is the one that doesn't work at all). Once you've done this, all your layouts will work just as they should.