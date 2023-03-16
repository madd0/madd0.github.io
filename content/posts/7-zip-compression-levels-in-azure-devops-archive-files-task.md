---
title: '7-Zip compression levels in Azure DevOps Archive Files task'
date: Thu, 30 Jan 2020 17:28:29 +0000
draft: false
tags: ['7-Zip', 'Azure DevOps', 'Azure Pipelines', 'English', 'Technology']
---

In an attempt to make my artifacts smaller, I recently chose to use 7-Zip compression, or `archiveType: 7z`, in an Archive Files task of an Azure DevOps YAML pipeline. [7-Zip provides 5 compression levels](https://sevenzip.osdn.jp/chm/cmdline/switches/method.htm#7Z): 1 (fastest), 3 (fast), 5 (normal), 7 (maximum) and 9 (ultra), as well as option 0, which doesn't compress anything.

I like YAML pipelines, because they live in my repo and I can use templates. However, the online editing experience is not particularly great. Sure, the online editor "assists" you when editing a simple file, but if you're referencing templates, you're out of luck (or at least I haven't found a way to edit a template and use the "assistant".)

Long story short, I'm editing a template (in a text editor) and I want to specify the compression level in my task. The official [Archive Files task documentation page](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/archive-files?view=azure-devops) unfortunately doesn't document the property that defines this. Luckily, a dummy pipeline and the "assistant" allowed me to quickly figure out that I wanted to set the `sevenZipCompression` property of the task. Of course, since the property wasn't documented, neither were the values that it accepted. So with a little patience and using [the task's source code](https://github.com/microsoft/azure-pipelines-tasks/blob/master/Tasks/ArchiveFilesV2/archivefiles.ts#L129) to confirm, I quickly came up with a table, which I decided to persist here for future reference:

Level

Descriptoin

`sevenZipCompression` value

Default

0

No compression

'none'

1

Fastest compressing

'fastest'

3

Fast compressing

'fast'

5

Normal compressing

'normal'

yes

7

Maximum compressing

'maximum'

9

Ultra compressing

'ultra'

7-zip compression levels for the Azure Pipelines Archive files task

A complete example of the task would look something like this:

```
\- task: ArchiveFiles@2
  displayName: 'Compress Files'
  inputs:
    rootFolderOrFile: '$(Build.BinariesDirectory)'
    includeRootFolder: false
    archiveType: '7z'
    sevenZipCompression: 'maximum'
    archiveFile: '$(Build.ArtifactStagingDirectory)/$(Build.BuildNumber).zip'
    replaceExistingArchive: true
```

Illustration: _[Emballages compressés](https://www.flickr.com/photos/photogestion/4430632949)_ by [](https://www.flickr.com/photos/photogestion/)[Daniel Hennemand](https://www.flickr.com/photos/photogestion/) is licensed under [CC BY-NC-ND 2.0](https://creativecommons.org/licenses/by-nc-nd/2.0/)