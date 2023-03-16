---
title: 'Windows Phone 7 : Introduction et installation des outils'
date: Mon, 13 Jun 2011 09:45:00 +0000
draft: false
tags: ['Developer Tools', 'Français', 'Software Development', 'Technology', 'Windows Phone 7']
---

Introduction
------------

![Windows Phone 7](http://madd0.files.wordpress.com/2011/06/windows_phone_7.jpg)La semaine dernière, on m’a demandé de parler au [WygDay](http://wygday.wygwam.com/) sur le développement Windows Phone 7 avec [Niels](http://www.stumpy.fr/). Lui, il a présenté le système à ceux qui ne le connaissaient pas et fait quelques démos sur les nouveautés que l’on peut trouver dans Mango—la nouvelle version qui sortira, a priori, au deuxième semestre. Moi, j’ai pris le pari de faire une application complète dans les 20 minutes qui restaient.

Evidemment, il s’agit d’une application plutôt simple—pas de MVVM, pas d’IoC ou d’injection de dépendances. Ce n’était pas la chasse aux mot clés à la mode, juste une application qui montre quelques concepts de base.

Etant donné qu’il y a eu un certain intérêt pour ces concepts, d’ailleurs, j’ai décidé que j’allais reprendre la démo ici en plusieurs billets courts. Voilà la “table de matières” qui reprend ma démo du WygDay :

1.  **Introduction et installation des outils**
2.  [Création d’une application et utilisation du contrôle Bing Maps](http://blog.madd0.com/2011/06/14/cration-dune-application-et-utilisation-du-contrle-bing-maps/ "Création d’une application et utilisation du contrôle Bing Maps")
3.  [Le GPS et les services de géolocalisation](http://blog.madd0.com/2011/06/15/le-gps-et-les-services-de-golocalisation/ "Le GPS et les services de géolocalisation")
4.  [Consommation d’un service OData](http://blog.madd0.com/2011/06/16/consommation-dun-service-odata-avec-windows-phone-7-mango/ "Consommation d’un service OData avec Windows Phone 7 “Mango”")
5.  [Ajout de punaises sur une carte Bing Maps](http://blog.madd0.com/2011/06/17/ajout-de-punaises-sur-une-carte-bing-maps/ "Ajout de punaises sur une carte Bing Maps")
6.  [Création de nouvelles pages et navigation](http://blog.madd0.com/2011/06/20/cration-de-nouvelles-pages-et-navigation-sur-windows-phone-7/ "Création de nouvelles pages et navigation sur Windows Phone 7")
7.  Création de vignettes sur la page d’accueil

Je suis sûr qu’en écrivant ces quelques articles, d’autres idées vont arriver et feront l’objet de nouveaux billets. Pour le moment, je vous invite à continuer votre lecture ci-dessous et à revenir tous les jours cette semaine pour la suite.

Installation des outils
-----------------------

[![get_the_free_tools](http://madd0.files.wordpress.com/2011/06/get_the_free_tools.jpg "get_the_free_tools")](http://create.msdn.com/)J’ai promis des billets courts, donc, après une longue introduction, je vais commencer cette série par un simple lien : [App Hub](http://create.msdn.com/).

C’est sur le App Hub que Microsoft a décidé de publier, gratuitement, tout ce qu’il faut pour écrire des applications pour Windows Phone 7 (et pour XBox, mais je vais essayer de rester sur le sujet qui nous intéresse).

En cliquant sur “[Download the free tools](http://create.msdn.com/en-us/home/getting_started)” (oui, pas de version française pour l’instant) vous avez le choix aujourd’hui entre les **Windows Phone Developer Tools 7.0** qui correspondent à la version actuelle de Windows Phone 7, ou les [**Windows Phone Developer Tools 7.1 Beta**](http://www.microsoft.com/downloads/details.aspx?FamilyID=77586864-ab15-40e1-bc38-713a95a56a05) pour la future version qu’on appelle “Mango”.

L’une comme l’autre vous permettront, a priori (sauf problèmes inattendus de la béta), d’écrire des logiciels pour la version actuelle qui pourront être publiées sur le Marketplace. Pour ma démo, on aura besoin de quelques fonctionnalités spécifiques à l’OS et/ou aux outils “Mango”, donc, si vous voulez suivre, je vous encourage à prendre la version 7.1 des outils. Vous y trouverez :

*   Microsoft Windows Phone Developer Tools 7.1 (Beta) — qui s’installeront sur une version Express de Visual Studio 2010 si vous n’avez pas ce dernier ou sur votre installation habituelle s’il est déjà sur votre machine.
*   L’émulateur Windows Phone (Beta)
*   Silverlight 4 SDK
*   Microsoft XNA Game Studio 4.0 Referesh Windows Phone Extensions
*   Microsoft Expression Blend SDK Preview pour Windows Phone 7.1
*   WCF Data Services Client pour Window Phone 7.1

Et ce sera tout pour aujourd’hui.

En attendant le billet de demain, je vous encourage à lancer Visual Studio et tester les nouveaux _templates_ de projet qui sont apparus ; notamment ceux sous la catégorie _Silverlight for Windows Phone_ dont le nom termine par _Application_. Vous pourrez les exécuter dans l’émulateur avec un simple _Ctrl+F5_ et commencer à vous familiariser avec.