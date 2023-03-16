---
title: 'Driver Azure Table Storage pour LINQPad'
date: Sun, 08 Jan 2012 15:03:54 +0000
draft: false
tags: ['Azure Table Storage', 'Français', 'LINQ', 'LINQPad', 'Software', 'Software Development', 'Technology', 'Windows Azure']
---

Vous connaissez [LINQPad](http://www.linqpad.net) ? Scott Hanselman le recommande systématiquement dans [liste annuelle d’outils pour développeurs](http://www.hanselman.com/blog/ScottHanselmans2011UltimateDeveloperAndPowerUsersToolListForWindows.aspx). En ce qui me concerne, je m’en sers pratiquement tous les jours—enfin, quand je développe.

[![linqpad](http://madd0.files.wordpress.com/2012/01/linqpad_thumb2.png "linqpad")](http://madd0.files.wordpress.com/2012/01/linqpad1.png)

À la base, c’est un logiciel qui vous permet d’exécuter des requêtes Linq :

[![linq_query](http://madd0.files.wordpress.com/2012/01/linq_query_thumb.png "linq_query")](http://madd0.files.wordpress.com/2012/01/linq_query.png)

Mais ça permet aussi d’exécuter des bouts de code arbitraires, juste pour voir ce que ça donne :

[![code_sample](http://madd0.files.wordpress.com/2012/01/code_sample_thumb.png "code_sample")](http://madd0.files.wordpress.com/2012/01/code_sample.png)

La fonctionnalité que j’utilise le plus c’est définitivement celle-ci, mais ces derniers temps je travaille de plus en plus avec [Windows Azure](http://www.windowsazure.com) et notamment [Table Storage](http://msdn.microsoft.com/en-us/library/windowsazure/dd179463.aspx). Bien que LINQPad supporte des requêtes sur [SQL Azure](http://msdn.microsoft.com/en-us/library/windowsazure/ee336279.aspx), j’étais un peu embêté quand il s’agissait d’effectuer rapidement des requêtes sur le Table Storage. Du coup, j’ai décidé d’écrire un driver pour le supporter !

Le driver permet d’ajouter des comptes de stockage (_storage accounts_) en tant que connexions LINQPad :

[![add_storage_account](http://madd0.files.wordpress.com/2012/01/add_storage_account_thumb.png "add_storage_account")](http://madd0.files.wordpress.com/2012/01/add_storage_account.png)

Une fois que vous avez ajouté le compte—qui peut être votre compte de développement local, si l’émulateur est activé, ou un compte sur le _cloud_—vous le verrez apparaitre dans la liste de connexions avec ses tables et leurs colonnes.

[![linqpad_tables](http://madd0.files.wordpress.com/2012/01/linqpad_tables_thumb.png "linqpad_tables")](http://madd0.files.wordpress.com/2012/01/linqpad_tables.png)

La suite c’est du LINQPad “comme d’habitude”. Enfin, si vous avez vos habitudes, sinon vous pouvez commencer par un clic droit sur une table pour insérer une des requêtes par défaut.

Evidemment, pour ce faire, il faut télécharger le driver. Vous avez deux choix :

*   Le code source, qui est disponible sur [GitHub](https://github.com/madd0/AzureStorageDriver).
*   Ou [le driver compilé](https://github.com/downloads/madd0/AzureStorageDriver/Madd0.AzureStorageDriver-v1.0.0-beta.lpx) (.LPX) à installer directement.

Petit _warning_ : on est en version 1.0.0-**beta**. Ça veut dire que je n’ai pas testé le code, mais qu’il a l’air de marcher. Si vous utilisez Azure Table Storage et LINQPad et que vous voulez tester le driver, tout feedback est bienvenu !