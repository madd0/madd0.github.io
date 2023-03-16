---
title: 'I have [finally] resumed work on amazOOP'
date: Mon, 06 Nov 2006 13:51:28 +0000
draft: false
tags: ['amazOOP', 'English', 'PHP']
---

So, most of my readers are not concerned by this post, but I’m still writing it for the occasional surfer coming from search engines and forums.

I have resumed work on my open-source project [amazOOP](http://amazoop.sourceforge.net). I just committed about 12000 lines of **alpha** code to [SVN](http://amazoop.svn.sourceforge.net/viewvc/amazoop/) so that you can see what the code is starting to look like.

Major changes:

*   **PHP 5**: I know most of the Web hasn’t migrated to PHP 5, but I have. The good news is that most of the code will be automatically generated, so, in theory, a PHP 4 version should be easily obtained in a couple of days with little effort if needed.
*   **Modular architecture**: I develop amazOOP for myself, but I also make it available to others, the problem with this is that “others” don’t necessarily work in the same environment that I do, and they might not be able to use amazOOP for the most trivial reasons (I’m thinking of those who mailed me asking if it was possible to use CURL). You can’t really see it now, but amazOOP will be modular, that means that the “module” that connects to the web service will be easily replaced if you need to use CURL, or the “module” that handles caching can be easily replaced if you want to use MySQL.
*   **Documentation**: I’m working on documentation from the beginning. Combined with the above (oh, and the SVN repository), this means that I (hopefully) won’t be the only person writing code for amazOOP, which in turn means that bug corrections and new features should be more frequent.
*   **No more configuration files**: amazOOP is supposed to be an object oriented API, so no more weird configuration files with undocumented arrays with arbitrary values. You’ll use objects to configure amazOOP. Of course, if you wish to store and/or initialize these objects in files, go ahead, that’s what I plan to do myself.
*   **Faster**: this version of amazOOP will use the latest version of Amazon’s web services, which, combined with better code, will should make amazOOP a lot faster.
*   **Support for France and Canada**: because I use the latest version of Amazon’s web services, Canadian and French Amazon shops will finally be supported.

I’ll continue to commit code to SVN as often as possible. I’m open to suggestions, so please don’t hesitate to use the blog and/or contact forms ([here](http://www.madd0.com/en/contact.php) and [here](http://sourceforge.net/sendmessage.php?touser=956883)) to get in touch with me.

As for [Awesom!](http://amazoop.sourceforge.net/awesom/), as soon as amazOOP is finished, I will be able to update the Mambo (or Joomla, another decision you have to help me make) component to make it faster and more stable.