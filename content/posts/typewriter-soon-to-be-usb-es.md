---
title: 'Máquina de escribir a punto de hacerse USB'
date: Fri, 14 Mar 2008 17:11:20 +0000
draft: false
tags: ['Curiosity', 'DIY', 'Français', 'Fun', 'Hardware', 'MAKE', 'Making', 'Projects']
---

[![Typewriter soon to be USB](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/TypewritersoontobeUSB_1.jpg)](http://www.flickr.com/photos/madd0/2331849634/)

Hace un rato compré una máquina de escribir (la de la foto) con única intención de, algún día, conectarla a mi computadora con un cable USB. Por supuesto, yo sé que una máquina de escribir sería un teclado muy ruidoso, pero a quién le importa? :P

También sé que, obviamente, otros lo han hecho antes, pero una vez más, a quién le importa?

[![S7300865](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/S7300865_thumb.jpg)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/S7300865.jpg)El primer paso fue comprar la máquina de escribir. Gracias a eBay, ya eso está hecho. Si se fijan bien, además notarán que la disposición del teclado es muy similar a mi teclado francés suizo que me gusta tanto.

La segunda etapa fue comprar un teclado USB corriente y destazarlo para conservar la única parte que me interesa: la tarjeta de circuitos. Como verán, un teclado es algo muy sencillo. Básicamente, cada vez que se presiona una tecla estamos cerrando un circuito. Cada tecla que se presiona cierra un circuito diferente, resultando en códigos diferentes que se envían a la computadora. Si abren un teclado, verán que contiene dos capas de plástico impresas y presionar una tecla lo que hace es unir las líneas impresas en esas dos capas. Cada capa tiene impresas líneas conductoras que terminan en uno de los contactos del circuito siguiente:

[![Mapping keys (3)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Mapping%20keys%20(3)_3.jpg)](http://www.flickr.com/photos/madd0/2330254111/)

Los conductores de una capa estarán conectados a los contactos llamados A hasta J (me salté la "I" porque se confunde fácilmente) y los de la otra capa estarán conectados a los contactos llamados 1 hasta 18, esto nos permite un total de 9 x 18 = 144 circuitos cerrados. Lo único que hace falta ahora es descubrir a cuales teclas corresponde cada circuito.

Hay dos formas de hacerlo:

*   Pueden seguirse las líneas conductoras de cada capa plástica desde la tecla hasta el contacto correspondiente, pero esto es largo y complicado porque hay muchas y las líneas son muy finas.
*   Puede usarse algo como un multímetro (o un pedazo de cable fino) para cerrar cada uno de los circuitos a mano mientras el teclado está conectado a la computadora.

Yo escogí la segunda opción. Así que escribí rápidamente una aplicación .NET que escucha teclas del teclado y muestra sus nombres, mientras yo cierro cada uno de los 144 circuitos. En realidad eran un poco menos, porque, si se fijan bien, el contacto A no está conectado. Este fue el resultado:

[![Key Matrix](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Key%20Matrix_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enTypewritersoontobeUSBlang_enlang__12920/Key%20Matrix.png)

Voy a tener que revisar esta matriz antes de soldar cualquier cosa, pero estoy seguro que es bastante precisa. La mayoría de nos nombres de las teclas son bastante obvios, pero para otros se necesita conocer la enumeración .NET [Keys](http://msdn2.microsoft.com/en-us/library/system.windows.forms.keys.aspx). Las teclas más molestas fueron las que llamé "Hibernate" y "Sleep" (B8, B9, F3 y H3) ya que cada vez me atrasaban un poco mientras esperaba que la computadora se "despertara".

Ahora lo único que hace falta es encontrar una forma de hacer que cada tecla de la máquina de escribir cierre el circuito correcto y tendré un máquina de escribir USB, pero eso es trabajo para otro día.