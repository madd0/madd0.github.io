---
title: 'Buscar un asterisco en Excel'
date: Sun, 11 Oct 2009 21:32:49 +0000
draft: false
tags: ['Español', 'Excel', 'Office 2007', 'Technology', 'Tips']
---

[![](https://farm4.staticflickr.com/3415/3579453701_f9f6e5055d_m_d.jpg)](https://www.flickr.com/photos/tetsumo/3579453701/)

El otro día estaba sentado en mi escritorio cuando, de pronto, alguien entró en la oficina e hizo la pregunta más extraña:

> Estamos trabajando en Excel y hay una columna de números de orden con una estrella al final y quisiéramos borrarla. ¿Alguien sabe cómo hacerlo?

Obviamente, todos respondimos en coro:

> ¡Pues, Ctrl+H (o Edición > Remplazar) y remplaza el carácter ‘\*’ por nada!

Excepto que, por supuesto, no funcionó. El problema: el asterisco (‘\*’) es un carácter especial cuando se hace una búsqueda en Excel; es un carácter comodín o de sustitución.

¿Pero, debe haber una forma de buscar un asterisco en Excel, no?

¡Por supuesto! ¡Cualquier cosa es posible en informática! Lo único que hay que hacer es utilizar una secuencia de escape, o sea, preceder el caracter especial de otro caracter especial; en nuestro caso es la tilde de la eñe (‘~’).

Así que solo queda buscar el texto ‘~\*’ (sin los apóstrofos, por supuesto) y remplazarlo por nada; eso borrará los asteriscos de su hoja de cálculo Excel.

(Photo [Tetsumo](http://www.flickr.com/photos/tetsumo/3579453701/) / [CC BY 2.0](http://creativecommons.org/licenses/by/2.0/))