---
title: 'Azure Labs commandlets on Windows x64'
date: Sun, 22 Mar 2009 09:37:06 +0000
draft: false
tags: ['Azure', 'English', 'Fix', 'PowerShell', 'Software Development', 'Technology', 'Windows', 'x64']
---

[![powershell](http://blog.madd0.com/images/WindowsLiveWriter/9fef72710387_9D58/powershell_thumb.png "powershell")](http://blog.madd0.com/images/WindowsLiveWriter/9fef72710387_9D58/powershell_2.png)I was doing the Hands on Labs from the [Azure SDK](http://www.microsoft.com/azure/sdk.mspx) the other day and one of them involves a task list that a very handy PowerShell commandlet is supposed to fill.

The problem?

`Registering commandlets... Add-PSSnapin : No Windows PowerShell Snap-ins are available for version 1. At C:UsersMadd0DocumentsAzureServicesKit-FebLabsAdvancedSQLDataServicesAssetsSDSSetup.ps1:17 char:13 + Add-pssnapin  <<<< AzureServicesManagement`

Now, why wouldn’t there be any snap-ins available for version 1? I can see the dll sitting there and I can only assume that Microsoft released code that works.

Easy!

As many other problems developers face these 32-to-64-bit-transition days, the missing snap-in just needed to be executed in a x86 environment, but I happen to work on Vista x64 (yep, a little masochistic, I know…).

The solution then is simply to open the console called Windows PowerShell (X86) and execute the SDSCreateStorage.cmd command there—don’t forget to run as Administrator.