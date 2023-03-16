---
title: 'Mise à niveau vers Windows NT 6.0 (alias Windows Vista)'
date: Sat, 06 Jan 2007 09:53:54 +0000
draft: false
tags: ['Français', 'Microsoft', 'Mozy', 'Office 2007', 'TDF 2007', 'Technology', 'Vista', 'Windows']
---

Ca y est, je l’ai fait ! Windows NT 6.0, ou Windows Vista (ou encore Windows VI, comme j’aime bien l’appeler) est, depuis hier soir, mon SE principal.

Ca s’est fait beaucoup plus tôt que prévu, mais XP ne m’a pas vraiment laissé le choix : j’ignore comment, mais la base de registre a été corrompue après une défragmentation du disque dur et je n’ai pas été assez intelligent pour la réparer correctement (j’aurais pu utiliser ma partition Vista RC2 pour rechercher une version propre du registre dans le dossier System Volume Information, mais à la place j’ai démarré XP avec un registre par défaut que j’ai récupéré en utilisant la Console de Récupération et qui a remplacé le registre qui marchait…)

Alors, comment ça s’est passé ? Allons-y pas à pas.

**Préparation**

J’ai commencé par sauvegarder ma partition XP complète sur un disque dur externe. Ca a pris une éternité, mais au moins j’étais sûr de ne pas perdre des données importantes. Cette sauvegarde et le fait que j’avais fait une sauvegarde complète avec [mozy](https://mozy.com/?code=SSKKSN) moins de 24 heures auparavant me rendaient assez confiant. Je n’avais pas de logiciel à désactiver ou désinstaller parce que, à part Windows et Office, la plupart de mes logiciels sont soit autonomes, open source et/ou gratuits. De toutes manières, j’aurais rien pu désinstaller puisque mon registre était tout neuf et ne savait rien sur ce qui était installé sur mon PC.

Le temps que tous mes fichiers soient copiés sur le disque dur externe il était déjà minuit. Mon DVD Vista et ma clé étaient prêts. Alors j’ai redémarré et commencé l’installation.

**Installation**

Je n’ai qu’une chose à dire à propos de l’installation :

Merci Microsoft pour la meilleure expérience d’installation que je n’aie jamais eue !

Certes, on ne peut pas sélectionner chacun des composants que l’on veut installer comme on peut le faire avec la plupart des distributions Linux. J’admets que l’installeur est un peu violent dans ses avertissements sur les effets des ce que vous êtres en train de faire (comme, ne pas fournir de clé par exemple), mais je m’en fous. L’interface est jolie… Ah non, attendez, j’ai un reproche concernant l’interface : c’est quoi cette idée de mettre le bouton “précédant” en haut à gauche de l’écran et le bouton “suivant” en bas à droite ? Et pourquoi une flèche pour l’un et du texte pour l’autre ? Si l’idée était de confondre l’utilisateur, c’est réussi ! A part ça, l’interface est jolie et à minuit et demie, Vista était installé !

J’ai déjà remercié Microsoft pour l’installation, mais j’ai encore des remerciements :

<démarrer sarcasme>Merci beaucoup l’Union Européenne !!!</fin sarcasme>

La clé Vista que j’ai eue avec MSDNAA se trouve être une clé pour Vista Business _N_. Que veut dire le _N_ ? C’est simple : pas de Windows Media Player. Grâce à un groupe de c\*\*\*\*\*\* à Bruxelles, Microsoft doit distribuer une version _N_ de son système d’exploitation sans le media player, ce qui me laisse, non pas sans media player sous Vista, parce que je peux en télécharger d’autre en ligne, mais sans le media player que **je veux** sous Vista : Windows Media Player 11 ! Bon j’arrête de déblatérer (ouais, je m’amuse avec Shift+F7, j’écris ceci sous Word 2007), je n’ai plus qu’à attendre février. J’espère à ce moment-là migrer vers Vista Ultimate ou, au moins, être capable de télécharger WMP 11…

**Autres logiciels**

Ensuite je me suis couché, mais ça ne vous intéresse pas, donc je passe au vrai point suivant : l’installation d’Office. J’ai téléchargé la version d’essai d’Office 2007 sur [TryMicrosoftOffice.com](http://www.trymicrosoftoffice.com) (pour ceux qui veulent télécharger en anglais, 90210 est le code postal de Beverly Hills en Californie ;) ) et j’ai installé Outlook, Word, Excel et PowerPoint. Ca aussi je l’intention de le mettre à jour en février (j’aurais pas trop choix, d’ailleurs ;) ).

Je voulais aussi installer le add-in pour enregistrer des PDFs et XPSs sous Office 2007, mais il refusait de s’installer parce que j’utilise une version d’essai d’Office. L’astuce : j’ai installé une version complète de OneNote 2007 avec ma clé MSDNAA et ensuite l’add-in s’est installé sans soucis pour toute la suite Office.

J’ai récupéré mes fichiers PST et j’ai configuré Outlook comme je l’aime bien. J’ai aussi restitué tous mes documents, y compris mes mots de passe que je gère maintenant avec [KeePass](http://keepass.info/).

J’ai aussi installé tout ce qui est messagerie instantanée (Skype, Windows Live Messenger et Google Talk) et je crois que c’est bon.

Ah, bien sûr, comment j’ai pu oublier ? J’ai aussi installé Microsoft Expression Graphic Designer (oui, la CTP de Septembre 2006) qui marche bien avec Vista RTM (j’ai pas vraiment testé le support XAML, par contre). Comment faire pour qu’il n’expire pas en avril ? <soupir>

La plupart des autres programmes que j’utilise tous les jours se trouvent dans D:Utils, entre autres mon [lecteur de PDF](http://www.foxitsoftware.com/pdf/rd_intro.php), le [logiciel pour les impressions d’écran](http://weblogs.asp.net/kennykerr/archive/2006/10/19/Window-Clippings-1.2.aspx), etc. et aucun ne nécessite d’installation ou quoi que ce soit d’autre.

**Programmes troublés**

Un programme peut-il être troublé ? C’est une discussion pour un autre jour… Parmi les programmes que j’ai installés il y en a qui ont du mal à s’adapter à leur nouvel environnement :

*   Visual Studio 2005 : j’ai installé Visual Studio 2005 Team Suite et Windows me dit qu’il y a des “compatibility issues” avec ce logiciel. J’espérais que le SP1 sorti récemment aller résoudre quelques uns des ces “issues”, mais je n’ai pas pu l’installer. Le SP1 “normal” comme la version Béta pour Vista affichent le message suivant :
    
    > “The upgrade patch cannot be installed by the Windows Installer service because the program to be upgraded may be missing, or the upgrade patch may update a different version of the program. Verify that the program to be upgraded exists on your computer and that you have the correct upgrade patch.”
    
    Je suppose qu’il faudra attendre la sortie du SP1 final pour Vista et ressayer.
    
    A part le message de Windows qui fait peur, Visual Studio à l’air de marcher comme il faut, donc je crois que je survivrai.
    
*   Plazer : j’utilise le logiciel Plazer de [Plazes.com](http://beta.plazes.com/) pour afficher l’endroit où je me trouve sur mon blog. Mais le programme ne semble pas capable de me localiser sous Vista. Bon, j’attendrai une prochaine version…
*   [Mozy](https://mozy.com/?code=SSKKSN) : pourquoi ? Ô pourquoi mozy ne marche-t-il pas encore sous Vista ? Comment vais-je faire mes sauvegardes ? Ils disent que la version pour Vista sera disponible en même temps que l’OS. J’espère que cela veut dire que ça sort le 1er février :)

**Autres choses bien (et pas si bien que ça)**

Quelles sont les autres choses bien ? Pour commencer, Vista tourne nickel sur mon PC. Je n’arrive pas à croire comment tout est fluide étant donné que mon PC n’a pas vraiment la configuration minimale requise pour Vista.

J’ai désactivé la sidebar, que je trouve être une application inutile qui ne sert qu’à consommer de la mémoire, mais Aero est activé (et j’ai même pas eu à utiliser le [hack](http://blog.madd0.com/2006/10/23/forcing-aero-on-computers-that-could-potentially-support-it-2/), qui l’aurait pensé).

J’aime bien que Vista Business n’installe pas les jeux Windows par défaut. Ca va sûrement être un grand gain pour la productivité mondiale ;)

Je n’aime définitivement pas la Plateforme RSS Windows, ou du moins, pas ses lecteurs. Je n’aime pas IE7 en tant que lecteur de flux RSS et je déteste définitivement Outlook 2007 : j’ai importé mon OPML avec Outlook et il a tout simplement ignoré ma structure de répertoires. Ni IE7 ni Outlook ne fournissent un moyen pour supprimer toutes les souscriptions facilement, donc j’ai créé un petit programme qui le fait grâce à la plateforme RSS Windows. IE7 a bien compris ce que j’avais fait, mais Outlook m’a complètement ignoré. Il affiche toujours tous mes flux et donc il faudrait que je les supprime tous un par un avec des messages d’erreur bizarres (du genre  “vous n’avez pas le droit de faire cela”, ouais, c’est ça, il croit être qui Outlook ?) alors que pense que je vais les laisser comme ça en attendant de trouver un moyen pour supprimer les 200+ flux…

J’aime bien les sons Vista et j’adore la barre de recherche qui marche plutôt bien. Je suppose que plus il aura le temps d’indexer mes fichiers, mieux ça va marcher.

J’écris ça sous Word 2007 d’ailleurs, et ça a l’air de marcher plutôt bien.

Donc voilà, j’utilise Windows Vista en tant que système d’exploitation principal et j’ai survécu le premier jour sans problèmes. On verra comment ça se passera lundi quand je retournerai donner cours.