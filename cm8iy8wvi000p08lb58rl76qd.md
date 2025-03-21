---
title: "When not buying from Apple"
datePublished: Fri Mar 21 2025 15:43:02 GMT+0000 (Coordinated Universal Time)
cuid: cm8iy8wvi000p08lb58rl76qd
slug: when-not-buying-from-apple
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/3JVnhF5kSKk/upload/df43600b72e5725ca4510739b0f80d0e.jpeg
tags: apple, device, macos, mdm, bypass

---

There’s a large secondary market for Apple/MAC devices because they hold value and deliver as promised being built on quality that lasts. Devices are generally hard to fake but sellers tend to embellish specifications or downplay usage.

However the thing you have to watch out for is [**Mobile Device Management (MDM)**](https://support.apple.com/en-ae/guide/deployment/depc0aadd3fe/web)**.** It’s a remote management tool that devices can be enrolled into from the factory. Implying ***Sealed*** devices.

Depending on how restrictive the policy is, It prevents you from even upgrading the Operating system. There are several means to enroll the device. If the MDM profile is visible in `Device Management` under *system preferences*, lucky! You easily delete it if you’re the admin or if you do a factory reset.

However the sinister hardware based MDM, comes up *after* you do a factory reset. When configuring your device to create accounts you need connect to the internet. This sends information to the servers\* which flag the device as locked to a company. You need to report or enroll it. The company will not release the device if you don’t have proper documentation. Most likely you won’t have it or it’s not valid. Luckily, there’s a [by-pass](https://github.com/assafdori/bypass-mdm) utility that you can use. However this will work till it won’t ([🤞](https://emojipedia.org/crossed-fingers#technical))

To validate if your misfortune, do a factory reset and be able to add an account yourself. Or if there is a dummy *admin or apple* account on the device, someone has already run the by-pass. Buyer beware!

### Serial number

To check usage, use the serial number that is etched into the device (or printed on the box) to confirm [coverage](https://checkcoverage.apple.com/) and the model of the item. You can also check the *About this mac* to confirm if the device is as advertised.

### Usage

Usage information is also available under the system report where you should check

1. `Power` for battery `Health Information` where *Cycle Count* and *Condition*
    
2. `Storage` for hard drive health where `S.M.A.R.T Status` should say *verified*
    
3. `Memory` for health where `Status` should say *ok* for *all* memory banks
    

Visually check the display for burn in and dead pixels.

Good luck, and enjoy your device, for the time being.

### References

* [Apple’s Mobile Device Management](https://support.apple.com/en-ae/guide/deployment/depc0aadd3fe/web)
    
* [Apple's Coverage](https://checkcoverage.apple.com/)
    
* [By-pass MDM for MacOS](https://github.com/assafdori/bypass-mdm)
    
* \*(“[deviceenrollment.apple.com](http://deviceenrollment.apple.com)” | “[mdmenrollment.apple.com](http://mdmenrollment.apple.com)” | “[iprofiles.apple.com](http://iprofiles.apple.com)”)