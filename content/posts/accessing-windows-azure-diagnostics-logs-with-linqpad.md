---
title: 'Accessing Windows Azure Diagnostics Logs With LINQPad'
date: Thu, 02 Feb 2012 12:41:04 +0000
draft: false
tags: ['Azure Table Storage', 'English', 'LINQ', 'LINQPad', 'Technology', 'Windows Azure']
---

If you are using [Windows Azure Diagnostics](http://msdn.microsoft.com/en-us/library/windowsazure/gg433048.aspx) with the [`DiagnosticMonitorTraceListener`](http://msdn.microsoft.com/en-us/library/windowsazure/hh411522.aspx) you will most likely have a table in your storage account called WADLogsTable with a ton of data in it. It can be a bit overwhelming.

A colleague and I wanted to get two simple pieces of information: an event's date and the corresponding message. Furthermore, we only wanted events that had happened today. Here's what we came up with using LINQPad and the Azure Storage Driver.

[![](http://madd0.files.wordpress.com/2012/02/linqpad_wadlogs.png?w=600&h=465 "LINQPad WADLogs")](http://madd0.files.wordpress.com/2012/02/linqpad_wadlogs.png)

First, make sure you're using a table storage account as your database. In my case, my connection is called `mycloudstorageaccount`.

Then simply perform your query. If you want to copy/paste, here's the text version:

\[code language="csharp"\] from l in WADLogsTable where l.PartitionKey.CompareTo(DateTime.Today.Ticks.ToString("d19")) > 0 select new { DateTime = new DateTime(l.EventTickCount.Value), l.Message } \[/code\]

Oh, and don't forget to check out the `SQL` tab if you are interested in the "low level stuff." It will show the actual URL that was used to query Windows Azure.

[![](http://madd0.files.wordpress.com/2012/02/sql_tab.png?w=600&h=133 "SQL Tab")](http://madd0.files.wordpress.com/2012/02/sql_tab.png)