---
layout: post
title: react-native-iap and Versioning
tags: [android, react-native, app]
---

A project we're working on uses react-native-iap for in app purchase. The version used for previous release was 5.4.1. But when I tried setting up the testing for payment, it hangs and won't show the payment dialog. Worse, in newer android even if you kill the app something is still loading and it won't respond and you have to reinstall the app (Might be due to some other factor though).

Upon inspection, the initialization was okay but `getSubscriptions` hangs and doesn't return at all. Google search suggest updating it to version 9.0.0 solves it. I tried but it had Amazon error and I thought I had to use lower versions, but lower versions without the above error still hangs. Apparently the fix for it is to add this line in `build.gradle`. It finally shows the payment dialog!

I guess the reason why the previous version doesn't work is because for new submissions to play store, I have to update the play store billing to version 4.

That took half day to solve.

Versioning problem is very annoying since most of the time the error message doesn't tell you any useful details. Upgrading package version also often breaks stuff so once I set up a project, I swear by the `package-lock.json`. I don't know how other projects manage with just doing `npm install` all the time since non major version change also breaks stuff.

I'm still not used to App development so I'm not really sure how Android manage the package versioning. Just last month I had to do long debugging only to find out that the gradle downloads new version by itself, specifying the version fixes it.

I know that keeping on using old version is not a good idea since outer world changes and the package will eventually have to be updated. And the thought of having to do that just dreads me out.