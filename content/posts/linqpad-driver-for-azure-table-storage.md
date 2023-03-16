---
title: 'LINQPad Driver for Azure Table Storage'
date: Mon, 09 Jan 2012 15:01:22 +0000
draft: false
tags: ['Azure Table Storage', 'English', 'LINQPad', 'Open Source', 'Technology', 'Windows Azure']
---

_I promise, this is the last you will see on this subject today (from my part, anyway). It's for those who were not online yesterday and/or are in a different time zone and/or didn't see [my post from yesterday](http://blog.madd0.com/2012/01/08/driver-azure-table-storage-pour-linqpad/ "Driver Azure Table Storage pour LINQPad") and/or don't speak French._

![](http://madd0.files.wordpress.com/2012/01/ase4_tables.png?w=150&h=108 "Azure Storage Explorer") I've been working quite a bit with [Windows Azure](http://www.windowsazure.com/) lately and particularly with [Table Storage](http://msdn.microsoft.com/en-us/library/windowsazure/dd179463.aspx). I used to use SQL Server Mangement Studio to work with SQL Server and I found [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/) (screenshot on the left), which is actually pretty good for working with all three storage options: queues, tables and blobs.

However, I'm a pretty heavy user of [LINQPad](http://www.linqpad.net/) (which has completely replaced SSMS for me for a while) and, although [it's totally possible to access Azure table storage with "standard LINQPad,"](http://consultingblogs.emc.com/jamiethomson/archive/2009/07/06/linqpad-and-azure.aspx) I was missing a few essential features, so I whipped up a LINQPad driver to easily query Azure Table Storage.

![](http://madd0.files.wordpress.com/2012/01/linqpad_tables.png "linqpad_tables.png")What does it do? It allows you to add storage accounts as connections in LINQPad. It supports the local emulator as well as actual cloud storage. With every connection, you get all the right references as well as a typed data context based on the account's tables.

I think I included everything you can expect from a typed data context, which will work like a charm with auto-completion if you have a LINQPad license. For anything that's not already there, the data context exposes a `TableClient` property that is a [CloudTableClient](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storageclient.cloudtableclient_members.aspx) instance. That should be enough to do anything you want.

There's also a couple of other "bonus" features, such as displaying the requested URL in the "SQL" tab of LINQPad:

![](http://madd0.files.wordpress.com/2012/01/query_request.png "query_request")

The whole thing is open sourced and [available on GitHub](https://github.com/madd0/AzureStorageDriver). It's even [compiled and packaged](https://github.com/madd0/AzureStorageDriver/downloads) if you're interested but don't want to deal with code.

If you work with Table Storage and LINQPad (if you haven't adopted LINQPad yet, it might be the right excuse to test it), don't hesitate to check the driver out. It would be nice if it got thoroughly tested and if I had feedback.