---
title: 'Typewriter soon to be USB'
date: Fri, 14 Mar 2008 17:11:16 +0000
draft: false
tags: ['Curiosity', 'DIY', 'English', 'Fun', 'Hardware', 'MAKE', 'Making', 'Projects']
---

[![Typewriter soon to be USB](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/TypewritersoontobeUSB_1.jpg)](http://www.flickr.com/photos/madd0/2331849634/)A while ago I bought a typewriter (the one in the picture) with the intention of one day being able to connect it to the computer using a USB cable. Sure, a typewriter will make for a noisy keyboard, but who cares? :P

I'm obviously not the first one to do it, but again, who cares?

[![S7300865](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/S7300865_thumb.jpg)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/S7300865.jpg) So, the first step was buying the typewriter. Thanks to eBay that's done. And, if you look carefully, you'll notice that the keyboard's layout is almost like my Swiss French layout that I like so much.

The second step was buying an actual keyboard and gutting it to keep only the part that interests me: the circuit board. You see, a keyboard is a pretty simple thing. Basically, every time you press a key you close a circuit. Every key you press closes a different circuit, resulting in different key codes being sent to the computer. If you open up a keyboard, you will see that pressing a key actually makes printed lines on two plastic layers touch. Each layer has printed conducting lines that end up connecting to one of the contacts in the circuit below:

[![Mapping keys (3)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Mapping%20keys%20(3)_3.jpg)](http://www.flickr.com/photos/madd0/2330254111/)

The conductors of one layer will connect to the contacts labeled A though J (I skip "I" because it's to easy to confuse) and the ones on the other layer will connect to the contacts labeled 1 though 18, bringing the number of possible closed circuits up to 9 x 18 = 144. All that's left now is to figure out what keystrokes correspond to each circuit.

There's pretty much two ways of figuring this out:

*   You can follow the conductor lines from each of the plastic layers from the place where the key strikes back to the corresponding contacts, but this is long and complicated because they're thin and there's plenty of them.
*   You can use something like a multi-meter (or a piece of wire) to close the circuits yourself while the keyboard is plugged to the computer.

I chose the latter. So I wrote a quick .NET application that listens to keystrokes and displays their name while I closed each of the 144 possible circuits. It was actually less, because if you look carefully, contact A isn't really connected to anything. This is what I came up with:

[![Key Matrix](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Key%20Matrix_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Key%20Matrix.png)

I will recheck this matrix before soldering anything, but it's pretty accurate as it is. Most of the key names are self explanatory, others need a little bit of knowledge of the .NET [Keys](http://msdn2.microsoft.com/en-us/library/system.windows.forms.keys.aspx) enumeration. The most annoying keys to find where those labeled "Hibernate" and "Sleep" (B8, B9, F3 and H3) which of course slowed things down a little bit while I waited for the computer to "wake up."

All that's left to do now is to figure out a way to make each key of the typewriter close the appropriate circuit and I'll have a USB typewriter, but that is work for another day.