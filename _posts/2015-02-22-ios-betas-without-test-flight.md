---
layout: post
title: iOS beta testing without TestFlight
date: 2015-02-22
---

Recently, [Apple acquired TestFlight](http://www.theverge.com/apps/2014/2/21/5434060/apple-buys-maker-of-the-ios-testing-platform-testflight), a service for deploying beta versions of iOS apps without going through the difficult Apple-approved process using Xcode. Since the aquisition, Apple have changed the TestFlight process to use iTunes and Xcode, and now it <strike>makes you want to tear your hair  out</strike> is "easy to do", [the documentation even says so!](https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/BetaTestingTheApp.html).

In fact, the new TestFlight is so easy to use that a plethora of new services have sprung up to replace it. Developers are leaving the new Apple product in droves<sup>[<span style='color:blue'>*citation needed*</span>]</sup>. Our team at work has started trying out some of these, and then thought to take matters into our own hands. We've only ever used the most basic feature of TestFlight (getting apps into the hands of users), so what about just doing that on our own?

How hard could it be, right?

Actually, as it turns out, not too hard at all.

**Test flighting without TestFlight**

There is a supported route for doing this, known as "Ad hoc deployment". Unfortunately, the Apple documentation on this kind of deployment is garbage. Most of information on this page comes from [this GitHub repository](https://github.com/gknops/adHocGenerate). The process simply involves sticking three files on a server.

N.B. If you plan to deploy to iOS 7.1 or above, these files must be served using **HTTPS**.

And here are the files:

**myapp.ipa**

Generate this from an Xcode archive using "Export" then "Ad Hoc Deployment". Just like TestFlight et. al., you'll still need to use a provisioning profile with all the UUIDs of your test devices to generate the archive.

**myapp.plist**

This shouldn't ever need to change, and should look something like this:

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>items</key>
        <array>
            <dict>
                <key>assets</key>
                <array>
                    <dict>
                        <key>kind</key>
                        <string>software-package</string>
                        <key>url</key>
                        <string>https://myappdeployment.com/myapp.ipa</string>
                    </dict>
                </array>
                <key>metadata</key>
                <dict>
                    <key>bundle-identifier</key>
                    <string>com.myapp.mobile</string>
                    <key>kind</key>
                    <string>software</string>
                    <key>title</key>
                    <string>myapp mobile</string>
                </dict>
            </dict>
        </array>
    </dict>
    </plist>

Just adjust the `url`, `bundle-identifier` and `title` values to taste.

**any HTML file**

An HTML file, which needs to contain a link to a URL like this:

    itms-services://?action=download-manifest&amp;url=https://myappdeployment.com/myapp.plist

 Once you've done all that, point your testers at that page, and they're good to go. When you have a new version, just replace the `.ipa` file, and let everyone know so they can re-download.
