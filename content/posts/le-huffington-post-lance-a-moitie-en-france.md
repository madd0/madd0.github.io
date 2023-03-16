---
title: 'Le Huffington Post lancé à moitié en France'
date: Fri, 27 Jan 2012 10:04:05 +0000
draft: false
tags: ['Bugs', 'Français', 'Huffington Post', 'RSS', 'Technology', 'Web Development']
---

![](http://madd0.files.wordpress.com/2012/01/huffington.png?w=150&h=39 "The Huffington Post")C'est une marque que peu connaissent en France, mais aux US _[The Huffington Post](http://www.huffingtonpost.com/), _ou juste _Huff Post_ pour faire court, est une source d'information pour quelque 35 millions de personnes par mois. Mais cela va probablement changer, puisqu'en début de semaine, _[Le Huffington Post](http://www.huffingtonpost.fr/)_ a vu le jour.

D'après [Arianna Huffington](http://fr.wikipedia.org/wiki/Arianna_Huffington), co-fondatrice de la version US et maintenant présidente et rédactrice en chef d'un groupe qui comprend une grande partie des sites les plus visités de l'autre côté de l'Atlantique :

> Le site incarnera l'ADN du Huffington Post, combinant les meilleures pratiques journalistiques des médias traditionnels avec la transparence, l'immédiateté et l'engagement des nouveaux médias - le tout avec une sensibilité typiquement française.

Le paragraphe précédent est extrait/traduit d'[un article _inceptionesque_ publié dans la version US pour annoncer la version FR](http://www.huffingtonpost.com/2012/01/23/le-huffington-post-debuts_n_1223689.html).

M'enfin, pourquoi dans le titre de mon billet je dis que le site est lancé "à moitié" en France ?

Suite au lancement, je me suis dit que je testerais bien ces "meilleures pratiques journalistiques", cette "transparence", etc. Mais, je ne sais pas vous, mais je ne visite jamais individuellement les sites où je m'informe—cela prendrait trop de temps—j’**agrège**. Mon premier réflexe a donc été de fournir l'URL du Huff Post FR ([http://www.huffingtonpost.fr](http://www.huffingtonpost.com/feeds/verticals/france/index.xml)) à Google Reader pour qu'il ajoute son flux RSS à mes souscriptions.

Premier bug : j'ai eu le flux de la version US… En effet, dans le code source la page principale du Huff Post FR on trouve ça :

\[code language="html"\] <link rel="alternate" type="application/rss+xml" title="Intégralité Des Flux" href="http://feeds.huffingtonpost.com/huffingtonpost/raw\_feed" /> <link rel="alternate" type="application/rss+xml" title="Dernières actus" href="http://feeds.huffingtonpost.com/huffingtonpost/LatestNews" /> <link rel="alternate" type="application/rss+xml" title="Blogs Sélectionnés" href="http://feeds.huffingtonpost.com/huffingtonpost/TheBlog" /> <link rel="alternate" type="application/rss+xml" title="Billets sélectionnés" href="http://feeds.huffingtonpost.com/FeaturedPosts" /> <link rel="alternate" type="application/rss+xml" title="Feed originaux" href="http://www.huffingtonpost.com/feeds/original\_posts/index.xml" />

<link rel="alternate" type="application/rss+xml" title="France Feed" href="http://www.huffingtonpost.com/feeds/verticals/france/index.xml" /> <link rel="alternate" type="application/rss+xml" title="France Blog" href="http://www.huffingtonpost.com/feeds/verticals/france/blog.xml" /> <link rel="alternate" type="application/rss+xml" title="France News" href="http://www.huffingtonpost.com/feeds/verticals/france/news.xml" /> \[/code\]

Un agrégateur n'étant pas capable de comprendre que quelqu'un a fait un bêtise, il prend le premier choix, qui ne correspond pas au bon site…

Bon, c'est pas grave, je comprends l'HTML, je vois qu'il y a un flux qui s'appelle "France Feed" (remarquez, au passage, que les flux français ont des noms en anglais et les flux anglais ont des noms en français) je prends donc son adresse et je l'ajoute à Google Reader.

Deuxième bug :

![](http://madd0.files.wordpress.com/2012/01/encoding.jpg?w=600&h=240 "encoding")

Il y a comme un petit problème d'encodage…

C'est dommage, je voulais vraiment tester ce site, mais je suppose qu'il faudra que j'attende que la version française ne soit plus en bêta pour le faire.