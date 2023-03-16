---
title: 'Visual Studio 2008: Où est passé l''Intellisense ?'
date: Mon, 30 Jul 2007 02:26:05 +0000
draft: false
tags: ['.NET', 'Français', 'Intellisense', 'Technology', 'Visual Studio']
---

Bien sûr qu'Intellisense existe toujours sous Visual Studio 2008. S'il y a quelque chose qui a changé, c'est peut être un certain nombre d'améliorations.

Par exemple, ça m'est arrivé plein de fois et je parie qu'à vous aussi : vous écrivez du code, la fenêtre Intellisense apparaît. Vous en êtes reconnaissant parce qu'elle vous permet en général de coder plus vite, mais à cet instant précis vous aimeriez qu'elle disparaisse pour voir ce qu'il y a derrière.

[![Visible Intellisense window](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_see_it_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_see_it.png)

Bon, à partir de Visual Studio 2008, le bonheur est à une touche de distance. Appuyez simplement sur ![Ctrl](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/ctrl_1.gif) et la fenêtre deviendra semi-transparente.

[![Transparent Intellisense window](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_dont_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_dont.png)

Mais bon, ce n'était pas ça le but de ce post. Je voulais parler de comment Intellisense ne marchait pas correctement sur mon installation de Visual Studio 2008 "Orcas" Beta 2 sur Vista et ce que j'ai fait pour le réparer.

Le problème était que, même si la fenêtre Intellisense ci-dessus apparaissait correctement, je ne pouvais pas voir la description de la méthode comme le montre l'image ci-après.

[![Method description](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/method_description_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/method_description.png)

Je n'avais pas la moindre idée de comment le réparer, mais en lisant différents articles sur Visual Studio 2008 je suis tombé sur [un post de ScottGu](http://weblogs.asp.net/scottgu/archive/2007/07/26/vs-2008-and-net-3-5-beta-2-released.aspx) où il donne la commande suivante :

[![visual_studio_reset_settings](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/visual_studio_reset_settings_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/visual_studio_reset_settings.png)

Remarquez que j'ai exécuté en mode Administrateur. Pourquoi ? Tout simplement parce que Scott a fait de même, mais je ne sais pas si c'est nécessaire. Tout ce que je sais c'est que la configuration de Visual Studio a été rétablie, qu'il s'est lancé et qu'Intellisense marchait. J'ai ensuite redémarré en mode "utilisateur normal" et Intellisense marche toujours. Donc voilà, je vais jouer avec VS 2008 moi maintenant.