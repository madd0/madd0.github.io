---
title: 'Visual Studio 2008: ¿Qué pasó con Intellisense?'
date: Mon, 30 Jul 2007 02:26:40 +0000
draft: false
tags: ['.NET', 'Español', 'Intellisense', 'Technology', 'Visual Studio']
---

Por supuesto que Intellisense todavía existe en Visual Studio 2008. Si algo ha cambiado, es tal vez un cierto número de mejoras.

Por ejemplo, ya me ha pasado miles de veces y apuesto a que a ustedes también: estoy escribiendo código, la ventana de Intellisense aparece. Aprecio que la ventana esté ahí porque generalmente me ayuda a programar más rápido, pero en este preciso momento me gustaría ver el código que está debajo.

[![Visible Intellisense window](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_see_it_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_see_it.png)

Pues, a partir de Visual Studio 2008, la felicidad está a tan sólo una tecla de distancia. Presione ![Ctrl](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/ctrl_1.gif) y la ventana se hará semitransparente.

[![Transparent Intellisense window](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_dont_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/now_you_dont.png)

Pero bueno, de esto no se trataba este post. Yo quería escribir sobre cómo Intellisense no funcionaba correctamente en mi Visual Studio 2008 "Orcas" instalado en Vista y cómo lo reparé.

El problema era que, aunque la ventana de Intellisense de la imagen de arriba aparecía correctamente, después no podía la descripción del método como en la imagen de abajo.

[![Method description](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/method_description_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/method_description.png)

No tenía ni idea de cómo arreglarlo, pero leyendo sobre Visual Studio 2008 encontré [un post de ScottGu](http://weblogs.asp.net/scottgu/archive/2007/07/26/vs-2008-and-net-3-5-beta-2-released.aspx) donde daba la instrucción siguiente:

[![visual_studio_reset_settings](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/visual_studio_reset_settings_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enVisualStudio2008WheredidIntellise_10A68/visual_studio_reset_settings.png)

Noten que la ejecuté en modo Administrador. ¿Por qué? Porque Scott hizo lo mismo, pero en realidad no sé si será necesario. Lo único que sé es que la configuración de Visual Studio se restableció, el programa se lanzó e Intellisense funcionó. Cuando volví a abrirlo en modo "usuario normal" Intellisense todavía funcionaba. Así que ahí lo tienen, ahora me voy a jugar con VS 2008.