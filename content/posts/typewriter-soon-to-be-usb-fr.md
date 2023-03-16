---
title: 'Machine à écrire sur le point de devenir USB'
date: Fri, 14 Mar 2008 17:11:19 +0000
draft: false
tags: ['Curiosity', 'DIY', 'Français', 'Fun', 'Hardware', 'MAKE', 'Making', 'Projects']
---

[![Typewriter soon to be USB](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/TypewritersoontobeUSB_1.jpg)](http://www.flickr.com/photos/madd0/2331849634/)

Il y a un moment j'ai acheté une machine à écrire (celle de la photo) avec l'intention d'un jour pouvoir la brancher sur mon ordinateur en USB. Oui, je sais, une machine à écrire fait un clavier très bruyant, mais on s'en fout, non? :P

Je ne suis évidemment pas la première personne à le faire, mais encore une fois, on s'en fout, non?

[![S7300865](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/S7300865_thumb.jpg)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/S7300865.jpg)Alors, la première étape était d'acheter la machine à écrire. Ca c'est fait, surtout grâce à eBay. Et si vous regardez bien la disposition du clavier est pratiquement identique à celle de mon clavier Suisse-français que j'aime autant.

La deuxième étape était d'acheter un vrai clavier afin de l'éventrer pour récupérer la seule partie qui m'intéresse : le circuit imprimé. Vous voyez, un clavier est un truc tout simple. En gros, chaque fois que vous appuyez sur une touche, vous fermez un circuit. Chaque touche va fermer un circuit différent, envoyant ainsi des codes différents à l'ordinateur. Si vous ouvrez un clavier, vous verrez que quand vous appuyez sur une touche vous mettez en contact des lignes imprimées sur deux couches plastiques. Sur chaque couche on a imprimé des lignes conductrices qui se terminent sur l'un des contacts du circuit ci-dessous :

[![Mapping keys (3)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Mapping%20keys%20(3)_3.jpg)](http://www.flickr.com/photos/madd0/2330254111/)

Les conducteurs d'une des couches vont vers les contacts A à J (je n'utilise pas "I" car c'est trop facile à confondre avec d'autres caractères) et ceux de l'autre couche vont vers les contacts que j'appelle 1 à 18, ce qui ramène le nombre de combinaisons de circuits fermés possibles à 9 x 18 = 144. Tout ce qu'il reste à faire c'est découvrir à quels circuits correspondent quelles touches.

Il y a deux manières pour ce faire :

*   Vous pouvez suivre chacune des lignes de l'endroit où la touche recherchée la frappe, jusqu'aux contacts, mais ceci est long et compliqué parce qu'il y a beaucoup de lignes et elles sont très fines.
*   Ou vous pouvez utiliser un multimètre ou quelque chose de similaire (un bout de câble par exemple) et fermer les circuits vous-même en ayant le clavier connecté à l'ordinateur.

J'ai choisi la deuxième option. J'ai donc rapidement écrit une petite application .NET qui écoute les touches du clavier et affiche le nom de celles-ci tandis que moi, je fermais chacun des 144 circuits possibles. Bon, en réalité il y en avait un peu moins, parce que, si vous regardez attentivement, vous remarquerez que le contact A, n'est pas vraiment connecté. Voici mes résultats :

[![Key Matrix](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Key%20Matrix_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Key%20Matrix.png)

Je vérifierai cette matrice à nouveau avant de souder quoi que ce soit, mais elle est assez précise telle qu'elle est. La plupart des noms des touches est assez explicite, mais pour certains il faut peut-être connaître un minimum l'énumération .NET [Keys](http://msdn2.microsoft.com/en-us/library/system.windows.forms.keys.aspx). Les touches les plus agaçantes étaient celles que j'ai appelées "Hibernate" et "Sleep" (B8, B9, F3 et H3) qui ont légèrement ralenti le processus.

Tout ce qu'il me reste à faire c'est de trouver un moyen pour que chaque touche de la machine à écrire ferme le bon circuit et j'aurai une machine à écrire USB, mais ça c'est du boulot que je remets pour plus tard.