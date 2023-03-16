---
title: 'Visual Studio 2008: Where did Intellisense go?'
date: Mon, 30 Jul 2007 02:26:24 +0000
draft: false
tags: ['English', 'Intellisense', 'Visual Studio']
---

Of course Intellisense is still there in Visual Studio 2008. If anything, it's undergone several nice improvements.

For example, it has happened to me thousands of times and I bet it has happened to you too: you are writing code, the Intellisense window pops up. You appreciate that it's there because you like how it helps you write code faster, but at that precise moment you'd really wish it would get out of the way so you could see the code that's underneath.

[![Visible Intellisense window](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_see_it_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_see_it.png)

Well, as of Visual Studio 2008, happiness is just one keystroke away. Just press ![Ctrl](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/ctrl_1.gif) and the window will become semi-transparent.

[![Transparent Intellisense window](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_dont_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_dont.png)

But well, this is not what this post is about. It's about how Intellisense was not working properly on my installation of Visual Studio 2008 "Orcas" Beta 2 running on Vista and what I did to fix it.

What was happening was that, although the little Intellisense window that you see above was appearing, I couldn't see the description of the method as shown below.

[![Method description](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/method_description_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/method_description.png)

I didn't really know how to fix it, but while reading around about Visual Studio 2008 I stumbled upon [a post by ScottGu](http://weblogs.asp.net/scottgu/archive/2007/07/26/vs-2008-and-net-3-5-beta-2-released.aspx) where I found the following command:

[![visual_studio_reset_settings](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/visual_studio_reset_settings_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/visual_studio_reset_settings.png)

Notice how I executed the command in Administrator mode. Why? Because so did Scott, but I don't really know if it's necessary. All I know is that Visual Studio had its configuration reset, launched and Intellisense worked. I restarted in "normal user" mode and Intellisense still works. So there you have it. I'm off to enjoy VS 2008 now.