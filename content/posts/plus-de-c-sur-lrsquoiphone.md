---
title: 'Plus de C# sur l’iPhone ?'
date: Fri, 09 Apr 2010 06:41:10 +0000
draft: false
tags: ['Apple', 'Français', 'Mobile Development', 'Mono', 'Software Development', 'Technology', 'Windows Phone 7']
---

[![clip_image001](http://blog.madd0.com/images/WindowsLiveWriter/PlusdeCsurliPhone_964C/clip_image001_thumb.jpg "clip_image001")](http://blog.madd0.com/images/WindowsLiveWriter/PlusdeCsurliPhone_964C/clip_image001_2.jpg)Avec la sortie hier du SDK pour l’iPhone OS 4, Apple surprend les développeurs en modifiant un paragraphe clé dans sa licence d’utilisation. Jusque là le paragraphe 3.3.1. lisait :

> 3.3.1 — Applications may only use Documented APIs in the manner prescribed by Apple and must not use or call any private APIs.

Formulé de cette manière, ce paragraphe empêche simplement les développeurs d’accéder aux **fonctionnalités** de l’iPhone qui ne sont pas exposées par les APIs publiques, documentées et donc supportées par Apple.

Cependant, le paragraphe en question a été légèrement remanié dans la dernière version de l’accord (je me permets de surligner quelques mots clés) :

> 3.3.1 — Applications may only use Documented APIs in the manner prescribed by Apple and must not use or call any private APIs. Applications must be **originally** written in **Objective-C, C, C++, or JavaScript** as executed by the iPhone OS WebKit engine, and only code written in C, C++, and Objective-C may compile and directly link against the Documented APIs (e.g., **Applications that link to Documented APIs through an intermediary translation or compatibility layer or tool are prohibited**).

Il n’est plus question uniquement de fonctionnalités ici, mais carrément du **choix du langage de programmation**. La liste est claire : si vous souhaitez développer pour l’OS 4, vos applications devront être écrites **à l’origine** en C, C++, Objective-C ou JavaScript—sinon, passez par une application web (ceci n’est pas dit explicitement, mais il est donc la seule alternative restante).

Que deviendra donc [MonoTouch](http://monotouch.net/), la solution Novell qui permet d’écrire des applications en C# pour l’iPhone ? Certes, le compilateur MonoTouch génère du code natif à la fin, mais l’application n’a pas été écrite dans l’un des langages autorisés à l’origine _et_ on utilise un outil intermédiaire pour générer l’application. La même question se pose pour le [compilateur pour iPhone](http://labs.adobe.com/technologies/flashcs5/appsfor_iphone/) qui devrait sortir avec Flash Professional CS5 puisqu’il se comporte de manière similaire.

L’arrogance de la société de Cupertino est telle qu’ils n’ont probablement rien à faire de la restriction de liberté totalement infondée pour les développeurs, mais je suis déçu quand même.

Enfin, essayons de voir les choses d’un point de vue positif : un potentiel tremplin pour le développement sur Windows Phone 7 ? ;)