---
title: 'Commandlets des Labs Azure sous Windows x64'
date: Sun, 22 Mar 2009 09:37:29 +0000
draft: false
tags: ['Azure', 'Fix', 'Français', 'PowerShell', 'Software Development', 'Technology', 'Windows', 'x64']
---

[![powershell](http://blog.madd0.com/images/WindowsLiveWriter/9fef72710387_9D58/powershell_thumb.png "powershell")](http://blog.madd0.com/images/WindowsLiveWriter/9fef72710387_9D58/powershell_2.png)

J’étais en train de travailler sur les Hands on Labs du SDK Azure l’autre jour et il y en a un qui concerne une liste de tâches qu’un commandlet PowerShell bien pratique est censée préparer.

Le problème ?

`Registering commandlets... Add-PSSnapin : No Windows PowerShell Snap-ins are available for version 1. At C:UsersMadd0DocumentsAzureServicesKit-FebLabsAdvancedSQLDataServicesAssetsSDSSetup.ps1:17 char:13 + Add-pssnapin  <<<< AzureServicesManagement`

Pourquoi n’y aurait-il pas de snap-in pour la version 1 ? Je vois la dll à côté et je ne peux que supposer que Microsoft va mettre à disposition du code qui marche.

Facile !

Comme beaucoup d’autres problèmes auxquels les développeurs doivent faire face pendant ces jours de transition du 32 au 64 bits, le snap-in manquant avait juste besoin d’être exécuté dans un environnement x86, mais je travaille sous Vista x64 (ouaip, un poil masochiste, je sais…).

La solution est donc très simple : ouvrez la console Windows PowerShell (X86) pour y exécuter la commande SDSCreateStorage.cmd—n’oubliez pas de l’exécuter en tant qu’Administrateur.