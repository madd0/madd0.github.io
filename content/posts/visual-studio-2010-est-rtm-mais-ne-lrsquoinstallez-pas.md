---
title: 'Visual Studio 2010 est RTM, mais ne l’installez pas !'
date: Tue, 13 Apr 2010 19:30:53 +0000
draft: false
tags: ['Français', 'Technology', 'Visual Studio 2010', 'Windows Phone 7']
---

![homeheroboxshot1_thumb_4F84E2E9](http://blog.madd0.com/images/WindowsLiveWriter/VisualStudio2010estRTMmaisnelinstallezpa_14A91/homeheroboxshot1_thumb_4F84E2E9_3.png "homeheroboxshot1_thumb_4F84E2E9") Enfin, ne l’installez pas si vous avez déjà commencé à faire du développement pour Windows Phone 7.

Malheureusement, la CTP des outils pours les développeurs Windows Phone 7 (WP Developer Tools CTP) **n’est pas compatible** avec la version finale (RTM) de Visual Studio 2010. Une mise à jour devrait être disponible sous quelques semaines.

Entre temps, si vous installez la RTM par-dessus votre installation existante des Developer Tools (DT), l’installation marchera, mais vous ne pourrez plus compiler vos projets Windows Phone. En revanche, si vous essayez d’installer les DT sur la RTM de VS2010, l’installation échouera.

Que faire ?

Vous pouvez être patients, après tout, ça fait longtemps qu’on attend VS2010 ; quelques semaines de plus ne signifieront probablement pas la fin du monde. Vous pouvez aussi installer la RTM dans une machine virtuelle, mais pas les DT, ces derniers ne peuvent pas être virtualisés.

Je suis un peu en retard avec mes billets sur Windows Phone, mais ne vous inquiétez pas, je me rattraperai et, dans la foulée, je vous tiens au courant de l’évolution des outils.

**UPDATE :** Téléchargez les [Windows Phone Developer Tools CTP (April 2010 Refresh)](http://download.microsoft.com/download/D/9/A/D9A6B6ED-D1CF-4FB3-86BD-62A55959175F/VMX/vm_web.exe) (lien direct vers l’installeur web) qui a encore des bugs (voire les [_release notes_](http://download.microsoft.com/download/D/9/A/D9A6B6ED-D1CF-4FB3-86BD-62A55959175F/ReleaseNotes.htm)) mais qui marche avec la RTM de Visual Studio 2010.