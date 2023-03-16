---
title: 'Compiler pour le Framework 1.1 sous Visual Studio 2005'
date: Tue, 03 Jan 2006 11:22:35 +0000
draft: false
tags: ['.NET', 'C#', 'Developer Tools', 'Français', 'Microsoft', 'Software Development', 'Technology']
---

Il est possible (on se demande si c'est utile, par contre?) de compiler des projets C# sous Visual Studio 2005 pour le Framework .NET 1.1. Plusieurs articles sur le Web expliquent comment le faire, mais ils sont en anglais. Je vais me contenter de traduire (plus ou moins fidèlement) [ce post](http://blogs.msdn.com/jomo_fisher/archive/2005/04/22/410903.aspx) de [Jomo Fisher](http://blogs.msdn.com/jomo_fisher/), developpeur dans la team MSBuild.

1.  Copiez le fichier mis à disposition [ici](http://blogs.msdn.com/jomo_fisher/articles/410896.aspx) (ou téléchargeable [ici](http://test.madd0.com/Images/2006/01/CrossCompile.CSharp.targets.txt)) dans le dossier `C:Program FilesMSBuild`. Appelez-le `CrossCompile.CSharp.targets.`
2.  Ouvrez le fichier projet (`*.csproj`) du projet C# que vous souhaitez compiler pour le Framework 1.1.
3.  Cherchez la balise `Import` et remplacez son attribut `Project` par : `Project="$(MSBuildExtensionsPath)CrossCompile.CSharp.targets"`
4.  Chargez le projet dans Visual Studio 2005.
5.  Le programme vous affichera un message d'avertissement vous indiquant que le fichier de projet a été modifié. Indiquez que vous souhaitez ouvrir le projet en mode normal.
6.  Dans le menu déroulant qui affiche 'Any CPU' (à côté du bouton 'Start Debugging') choisissez l'option 'Configuration Manager'.
7.  Dans la fenêtre qui s'ouvre, sous la colonne 'Platform', choisissez '.NET 1.1' et fermez la fenêtre.
8.  Pour vérifier que vous compilez bien pour la version 1.1 du Framework, essayez de compiler un projet qui contient des spécificités de la version 2, par exemple: `using System.Collections.Generic`, ou `public partial class...`