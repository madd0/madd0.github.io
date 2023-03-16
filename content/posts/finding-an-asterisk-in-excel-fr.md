---
title: 'Rechercher un astérisque sous Excel'
date: Sun, 11 Oct 2009 21:32:02 +0000
draft: false
tags: ['Excel', 'Français', 'Office 2007', 'Technology', 'Tips']
---

[![](https://farm4.staticflickr.com/3415/3579453701_f9f6e5055d_m_d.jpg)](https://www.flickr.com/photos/tetsumo/3579453701/)J’étais assis à ma place quand, soudain, quelqu’un rentre dans le bureau de l’informatique avec la question la plus étrange :

> On est sur Excel et on a une colonne avec numéros de commande qui se finissent tous par une étoile et on aimerait la virer. Quelqu’un sait comment on fait ?

Évidemment, la réponse en chœur a été immédiate :

> Ben, Ctrl+H (ou Edition > Rechercher) et tu remplaces le caractère ‘\*’ par rien du tout !

Sauf qu’évidemment, ça ne marche pas. Le piège : l’astérisque (‘\*’) est un caractère spécial lorsque l’on fait une recherche sous Excel ; il s’agit d’un caractère générique ou de substitution.

Mais il doit y avoir un moyen de trouver un astérisque dans une cellule Excel, quand même, n’est-ce pas ?

Évidemment ! Tout est possible en informatique ! Il suffit pour cela “d’échapper” le caractère spécial, c’est à dire, le précéder d’un autre caractère spécial ; dans notre cas, c’est le tilde (‘~’).

Cherchez donc la chaîne ‘~\*’ (sans les apostrophes, évidemment) et remplacez-la par rien du tout, cela effacera vos astérisques dans votre feuille Excel.

(Photo [Tetsumo](http://www.flickr.com/photos/tetsumo/3579453701/) / [CC BY 2.0](http://creativecommons.org/licenses/by/2.0/))