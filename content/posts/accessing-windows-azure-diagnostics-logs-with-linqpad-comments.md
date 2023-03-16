---
title: 'Accessing Windows Azure Diagnostics Logs With LINQPad'
date: Thu, 02 Feb 2012 12:41:04 +0000
draft: false
tags: ['Azure Table Storage', 'English', 'LINQ', 'LINQPad', 'Technology', 'Windows Azure']
---


#### 
[Mauricio Diaz Orlich](http://blog.madd0.com/ "mauricio.diazorlich@gmail.com") - <time datetime="2014-09-12 14:10:43">Sep 5, 2014</time>

I haven't used Azure logs in a while, so maybe the name of the table changed. Isn't there a table in your list with a similar name?
<hr />
#### 
[Mauricio Diaz Orlich](http://blog.madd0.com/ "mauricio.diazorlich@gmail.com") - <time datetime="2014-10-03 11:20:43">Oct 5, 2014</time>

Hi, the plugin uses the Azure SDK to query all tables for the specified account. It does not filter them in any way. I don't currently have access to an account that uses Azure Diagnostics so I cannot it try it myself. Does the plugin show all other tables present in the account?
<hr />
#### 
[Comp]( "prog@mailinator.com") - <time datetime="2014-09-07 09:43:47">Sep 0, 2014</time>

Hello, I could not access the local WADLog table. I have - wadlogs table with log entries (Azure Management Studio shows them). - storage account is correct because the Tables part is appears in LinqPad - Im using the Azure Storage Driver of course - but I get the following The name 'WADLogsTable' does not exist in the current context Do I need something additional to access the Diagnostic part besides the Tables ? Thanks in advance. Comp.
<hr />
#### 
[Comp]( "comp@mailinator.com") - <time datetime="2014-09-30 16:03:04">Sep 2, 2014</time>

Hello Diaz, Since then I noticed that, LinqPad doesn't shows the 'WADLogsTable' in the table list, but its exists according to Azure Storage Management Studio. Did you have the same situation as well ?
<hr />
