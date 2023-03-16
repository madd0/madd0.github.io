---
title: 'Opening twhirl Links in Google Chrome'
date: Thu, 06 Nov 2008 10:41:03 +0000
draft: false
tags: ['Chrome', 'English', 'Google', 'Internet', 'Internet Explorer', 'Technology', 'Tips', 'Twhirl', 'Twitter']
---

![Twhil links to Chrome](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/twhirl_links_3.png "Twhil links to Chrome")

In spite of its bugs, I’ve been using [Google Chrome](http://www.google.com/chrome) as my main browser for a while now; mainly because it is generally fast and because it allows me to kill Flash whenever it bugs (often) without having to kill the whole browser.

I also use Windows Vista because I like it and it doesn’t feel slower than XP even on my computer.

Finally, I use [twhirl](http://www.twhirl.org/) to follow my [Twitter](http://www.twitter.com) friends. It’s far from perfect, because I’d like to have a single client that allows me to follow not only Twitter but all the social networks in which I might have an account, but twhirl does a good job in the meanwhile.

One thing that’s bothered me from the beginning though—and I don’t know if this is a Windows (Vista?), twhirl or Chrome bug—is that whenever I click on a link on twhirl, it will open in Internet Explorer instead of Chrome, which is set up as my default browser. I tried different settings, but I didn’t find a solution until today, so I’m sharing it here because I’m sure others might be having the same problem.

(**Warning:** this solution involves modifying the Windows registry, which if done incorrectly might prevent your machine from working properly. Following my instructions carefully should be safe, but use at your own risk.)

1.  Open the Registry Editor by typing **regedit** in the Windows Start Menu. [![regedit](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/start_menu_thumb.png "regedit")](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/start_menu_2.png) You may see a confirmation window if UAC is enabled on your computer.
2.  Verify that the key **HKEY\_CLASSES\_ROOTChromeHTML** exists. [![ChromeHTML](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/Registry%20Editor%20(2)_thumb_1.png "ChromeHTML")](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/Registry%20Editor%20(2)_4.png) If this key doesn’t exist, you can stop reading here.
3.  Look for the key **HKEY\_CLASSES\_ROOT.htm** and change the **(default)** value to **ChromeHTML**. Repeat for **HKEY\_CLASSES\_ROOT.html**. [![ChromeHTML](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/Registry%20Editor%20(5)_thumb.png "ChromeHTML")](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/Registry%20Editor%20(5)_2.png)

That should do it!

Alternatively, you can also import this file into your registry: [correct\_chrome.reg](http://blog.madd0.com/images/WindowsLiveWriter/lang_enOpeningtwhirlLinksinGoogleChromel_9C17/correct_chrome.txt)