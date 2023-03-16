---
title: 'Commandlets de los Labs Azure en Windows x64'
date: Sun, 22 Mar 2009 09:37:28 +0000
draft: false
tags: ['Azure', 'Español', 'Fix', 'PowerShell', 'Software Development', 'Technology', 'Windows', 'x64']
---

[![powershell](http://blog.madd0.com/images/WindowsLiveWriter/9fef72710387_9D58/powershell_thumb.png "powershell")](http://blog.madd0.com/images/WindowsLiveWriter/9fef72710387_9D58/powershell_2.png)

El otro día estaba trabajando en los Hands on Labs del SDK Azure y hay uno que tiene que ver con una lista de tareas que un commandlet PowerShell bastante práctico tenía que preparar.

¿El problema?

`Registering commandlets... Add-PSSnapin : No Windows PowerShell Snap-ins are available for version 1. At C:UsersMadd0DocumentsAzureServicesKit-FebLabsAdvancedSQLDataServicesAssetsSDSSetup.ps1:17 char:13 + Add-pssnapin  <<<< AzureServicesManagement`

¿Por qué no habría un snap-in para la versión 1? Ahí veo la dll y tengo que suponer que Microsoft va a sacar código que funciona.

¡Fácil!

Como muchos otros problemas que los desarrolladores deben enfrentar en estos días de transición entre 32 y 64 bits, el snap-in que falta nada más necesitaba ser ejecutado en un ambiente x86, pero yo trabajo en Vista x64 (sí, yo sé, un toque masoquista…).

Así que la solución es simplemente abrir la consola Windows PowerShell (X86) y ejecutar SDSCreateStorage.cmd ahí—no olvide ejecutarlo como Administrador.