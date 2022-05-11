---
layout: post
title: Apple App Developer Account
tags: [apple, ios, app]
---

Some notes on the research that I found out about Apple Developer Account.

- Anyone can use their Apple ID for a [free Apple Developer Account](https://developer.apple.com/forums/thread/71283)
- This allow debugging/installing the app on iOS device by connecting it with USB to the Mac with the XCode
- Push Notifications require [a paid account](https://developer.apple.com/forums/thread/127698), ie. ADP (Apple Development Program) membership
- Paid developer account can share access from apple store connect website
  - It needs to be an `Organization` account to be able to give access to certificates
  - `Individual` account cannot do this
- It is a convention that the owner of the app has the paid account even though they are not the one who develop it
  - The developer's Apple ID then gets added into their account given certain permissions so that they can develop and release the app
  - The owner [has to be the one](https://developer.apple.com/forums/thread/114334) who adds the apple ID though
- An Apple ID can be a user in [multiple Apple](https://stackoverflow.com/a/1820746) [Developer Account](https://stackoverflow.com/questions/57162432/ios-developer-account-multiple-apps-for-multiple-clients#comment100842293_57162432)

### More References regarding Apple Developer Accounts
- [How to add development members to Apple Developer Program](https://www.zaico.co.jp/engineer/apple-developer-program-howto-add-member/)
- [Invite Salesforce to Your App Store Connect Account](https://help.salesforce.com/s/articleView?id=sf.branded_apps_gather_private_ios_invite_sfdc.htm&type=5)
- [Your client's developer accounts vs. your own
](https://www.goodbarber.com/blog/your-client-s-developer-accounts-vs-your-own-a856/)
- [Do both the developer and account holder need paid Apple Developer accounts?](https://stackoverflow.com/questions/66186037/do-both-the-developer-and-account-holder-need-paid-apple-developer-accounts)
- Oh only now I found out that Apple has [an official guide](https://help.apple.com/developer-account/#/dev3e8818774)
