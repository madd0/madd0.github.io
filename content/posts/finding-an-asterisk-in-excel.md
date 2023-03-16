---
title: 'Finding an Asterisk in Excel'
date: Sun, 11 Oct 2009 21:32:14 +0000
draft: false
tags: ['English', 'Excel', 'Office 2007', 'Technology', 'Tips']
---

[![](https://farm4.staticflickr.com/3415/3579453701_f9f6e5055d_m_d.jpg)](https://www.flickr.com/photos/tetsumo/3579453701/)I was sitting at my desk when, suddenly, someone came in the office and asked the weirdest question:

> We’re working on Excel and there’s a column with order number that end with a star and we’d like to remove it. Does anyone know how?

Obviously, we all immediately responded in choir:

> Why, Ctrl+H (or Edit > Replace) and you replace character ‘\*’ with nothing!

Except that, obviously, it didn’t work. The problem: the asterisk (‘\*’) is a special character when you are trying to find something in Excel; it’s a wildcard or substitution character.

But there has to be a way to find an asterisk in an Excel cell, isn’t there?

Of course! Everything is possible with computers! All you have to do is “escape” the special character, i.e., precede it with another special character; in our case, it’s the tilde (‘~’).

Look for the string ‘~\*’ (without the apostrophes, of course) and replace it with nothing at all; that will delete the asterisks from your Excel worksheet.

(Photo [Tetsumo](http://www.flickr.com/photos/tetsumo/3579453701/) / [CC BY 2.0](http://creativecommons.org/licenses/by/2.0/))