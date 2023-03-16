---
title: 'Tout ce que vous vouliez savoir sur Windows Phone 7'
date: Mon, 05 Apr 2010 16:07:14 +0000
draft: false
tags: ['Français', 'Microsoft', 'Mobile Development', 'Technology', 'Windows Phone 7']
---

Et si jamais je ne vous dis pas tout dans ce billet, ne vous inquiétez pas, [abonnez-vous au flux RSS](http://feeds.feedburner.com/madd0), je vais continuer à écrire sur ce sujet le plus souvent possible.

Aujourd'hui je vais être généraliste, je suis sûr que beaucoup veulent en savoir plus sur Windows Phone 7 sans pour autant être développeurs. À l'avenir mes billets seront plus orientés vers le développement sur cette nouvelle plateforme, bien que je me permettrai certains billets à contenu plus éditorial sur le Marketplace, certains choix de la plateforme, etc. Après tout, c'est mon blog.

![](/images/040510_1807_Toutcequevo1.png)

**Commençons donc par le début : qu'est-ce que Windows Phone 7 ?**

Jusqu'il y a quelques jours, ça s'appelait [Windows Phone 7 Series](http://www.windowsphone7series.com/) :

![](/images/040510_1807_Toutcequevo2.png)

Il s'agit de la nouvelle plateforme pour téléphones mobiles développée par Microsoft. Contrairement à l'[iPhone](http://www.apple.com/iphone/) d'Apple, **il ne s'agit pas un téléphone**. Comme [Android](http://www.android.com/), il s'agit plutôt d'une plateforme de développement pour téléphones mobiles. Cela comprend donc un **système d'exploitation**, [**_middleware_**](http://fr.wikipedia.org/wiki/Middleware), des **applications** de haut niveau (e-mail, galeries photo, etc.) et un moteur d'exécution d'applications **Silverlight et XNA**. De plus, Microsoft fournit un environnement de développement riche à souhait (et gratuit, soit dit en passant) comprenant une version dédiée de Visual Studio 2010, Blend, un émulateur, etc. ; j'en parlerai plus en détail dans un prochain billet.

Cette nouvelle plateforme vient succéder à Windows Mobile dans ses différentes versions. Alors que ces derniers systèmes d'exploitation sont basés sur le noyau Windows CE 5, Windows Phone 7 est basé sur Windows CE 6, comme le Zune HD. D'ailleurs, vous allez voir que c'est loin d'être le seul point commun avec le baladeur numérique de Microsoft.

L'interface graphique et, plus généralement, l'expérience utilisateur—un point qui n'a jamais été vraiment bien géré dans les versions précédentes, souvent laissé aux constructeurs ou OEM—ont été totalement revues. L'interaction tactile devient une priorité—les terminaux devront supporter au moins quatre points de contact simultanés d'ailleurs— et le téléphone s'intègre aux réseaux sociaux tels que Facebook, Xbox Live, etc.

**Les terminaux (le hardware)**

Comme avant, Microsoft ne fabriquera pas de téléphone, mais cette fois-ci les constructeurs devront suivre un certain nombre de règles pour embarquer le nouveau système d'exploitation. Des prototypes préparés par Asus, [LG](http://www.engadget.com/2010/02/27/exclusive-lgs-windows-phone-7-series-early-prototype-unveiled/) et [Samsung](http://www.engadget.com/2010/03/15/samsung-windows-phone-7-series-handset-makes-the-scene/) ont été montrés à [MIX10](http://live.visitmix.com/) et utilisés pour les démos.

Les spécifications exactes ne sont pas disponibles au moment où j'écris ces lignes, mais on sait déjà que tous les téléphones Windows Phone 7 posséderont au minimum :

*   Un écran large de 800 x 480 pixels (WVGA) ou 480 x 320 (HVGA)—bien que seulement les premiers seront disponibles lors de la sortie, les derniers visent à réduire le coût des terminaux par la suite.
*   Un écran capacitif capable d'identifier minimum quatre points de contact.
*   Six boutons _hardware_ : Démarrer (_Start_), Retour (_Back_), Recherche (_Search_ ; intégré au « moteur décisionnel » Bing), un bouton pour l'appareil photo, un autre pour mettre sous tension l'appareil, et enfin, le volume.
*   CPU : ARM v7 Cortex/Scorpion
*   Un chipset graphique supportant DirectX 9.
*   256 Mo de mémoire vive (RAM) et 8 Go de stockage Flash.
*   Capteurs : A-GPS, accéléromètre, boussole, lumière, proximité
*   WiFi
*   Radio FM
*   Appareil photo 5 mégapixels avec flash

Les constructeurs pourront choisir, évidemment, d'améliorer ces spécifications et/ou d'ajouter des caractéristiques pour se distinguer ; par exemple, le [prototype LG](http://www.engadget.com/2010/02/27/exclusive-lgs-windows-phone-7-series-early-prototype-unveiled/) possède un clavier physique.

**L'expérience utilisateur**

Si vous connaissez Windows Mobile, oubliez tout ce que vous avez déjà vu.

Les équipes responsables d'imaginer le nouveau téléphone ont conçu une interface totalement différente de tout ce qui était fait avant chez Microsoft, tout en s'inspirant du travail fait avec Zune et Windows Media Center, ainsi que les graphismes et typographies utilisés dans les transports publics ; ils ont appelé ceci « Métro UI ». Je parlerai plus sur Métro dans un prochain billet.

![](/images/040510_1807_Toutcequevo3.png)L'**écran de démarrage** reprend les principes de minimalisme et de mouvement dictés par Métro. Il est découpé en **tuiles** (ou carreaux, ou briques, je ne sais pas encore comment le mot _tiles_ va être traduit en français) **animées** qui permettent d'obtenir des **informations d'un coup d'œil et en temps réel** en plus d'accéder plus facilement à vos applications préférés ou vos **centres d'intérêt** (je ne sais pas comment ils vont traduire le mot _hub_ non plus). Les tuiles affichent aussi ce qui est le plus cher à l'utilisateur : ses contacts, ses photos, etc.

Le même esprit est repris par l'**écran de verrouillage**. Une grande photo occupe la totalité de l'écran et par dessus sont affichées la date et l'heure ainsi que les prochains rendez-vous, les appels manqués, etc. : un écran de verrouillage informatif.

Vous aurez remarqué dans les quelques captures d'écran dans cet article l'absence les bordures ou de fenêtres, notamment dans la première, le « centre d'intérêt » (promis, dès que j'ai la terminologie française, je vous tiens au courant) _People_, que j'appellerai Contacts. Dans cette capture on voit bien le concept de **panorama** : un écran qui dépasse les limites de l'écran physique.

Je ne m'attarderai pas plus sur l'expérience utilisateur, mais on y reviendra dans des articles ultérieurs.

**Les applications et les centres d'intérêt intégrés**

On en sait peu aujourd'hui sur les applications qui seront livrées avec le téléphone et ce qu'on a vu n'est pas encore finalisé, toutefois certaines applications ont déjà été confirmées :

*   **E-mails** : l'application a été optimisée pour être utilisée avec l'écran tactile, comme c'est déjà le cas chez d'autres constructeurs. Plus intéressant, l'application supportera plusieurs comptes de messagerie simultanément, y compris plusieurs comptes Exchange. Gmail, Yahoo ! et Hotmail seront aussi supportés.
*   **Calendrier** : très spartiate et très différent des autres agendas qu'on a pu connaître. À tester.
*   **SMS** : support pour SMS et MMS en mode portrait et paysage. Par contre, ma fonctionnalité préférée n'est pas spécifique à l'application, mais plutôt au clavier virtuel. Il s'agit d'un panel proposant un grand nombre de _smileys_. J'y reviendrai dans un prochain article qui abordera le clavier.
*   **Téléphone** : même si j'ai déjà vu des appels être passés depuis la liste de contacts, et un téléphone recevoir un appel, je ne peux pas dire que j'ai déjà vu le téléphone marcher. J'espère avoir plus d'informations prochainement.
*   **Contacts** : une liste de contacts très épurée dans laquelle on peut naviguer avec des gestes simples ou en utilisant le bouton de recherche.
*   **Navigateur** : une toute nouvelle version d'Internet Explorer différente de celle disponible sur Windows Mobile ou sur Zune capable de réagir à des gestes multitouch usuels, navigation par onglets et exécution de Javascript. En revanche, ni Flash ni Silverlight ne seront supportés.
*   **Recherche** : si le bouton recherche n'est pas utilisé de manière personnalisée dans une application, il dirigera l'utilisateur vers le moteur décisionnel Bing ; elle sera donc aussi utile que l'outil en ligne (qui évolue rapidement, mais n'est toujours pas mon premier choix). Je ne sais pas si ceci sera configurable.
*   **Cartographie** : un point clé sur tous les smartphones aujourd'hui, Windows Phone 7 utilisera Bing Maps pour la navigation et cartographie.

![](/images/040510_1807_Toutcequevo4.jpg)Le centre d'intérêt **Contacts** (je continue à inventer des noms, n'ayant pas de terminologie officielle sous la main) présente les contacts Exchange, Gmail, Yahoo, Facebook, Twitter, etc. et agrège des informations sur les contacts, leurs statuts, photos, etc.

![](/images/040510_1807_Toutcequevo5.jpg)Le centre **Images** agrège aussi bien les photos et images se trouvant sur le téléphone que vos photos sur Internet et celles publiées par vos contacts sur les réseaux sociaux.

![](/images/040510_1807_Toutcequevo6.jpg)Le centre **Jeux** intègre Xbox Live, y compris vos points et le même avatar que vous pouvez avoir sur votre Xbox. Il permet aussi l'accès aux jeux installés sur le téléphone.

![](/images/040510_1807_Toutcequevo7.jpg)Le centre **Musique + Video**, ou multimédia (je continue à inventer les noms) ressemble beaucoup à l'expérience du Zune HD. Il permet l'accès à la musique et aux vidéos que se trouvent sur le téléphone. Vous pourrez acheter de la musique depuis ici aussi.

![](/images/040510_1807_Toutcequevo8.jpg)Le centre **Marché d'applications**, le _marketplace_. Ici vous pourrez acheter et télécharger des applications. Ce sera le seul moyen d'installer des applications sur un Windows Phone (avec sa contrepartie PC bien sûr). Il gère aussi les mises à jour et, si le développeur de l'application le supporte, il vous proposera aussi des versions d'évaluation.

![](/images/040510_1807_Toutcequevo9.jpg)Le centre **Office** (je pense que ce nom est bon) proposera des applications que nous connaissons déjà, telles que OneNote, Word, Excel, … et accès à SharePoint. Malheureusement, je n'ai pas plus de détails en ce moment.

[Des **applications tierces** ont déjà été montrées, notamment lors du MIX10](http://windowsteamblog.com/blogs/wpdev/archive/2010/03/30/demo-apps-from-mix10-on-windows-phone-7.aspx).

**Les points qui prêtent à controverse**

Dès son annonce, il était évident que Windows Phone 7 serait comparé aux autres acteurs du marché d'aujourd'hui, notamment l'iPhone et les périphériques sous Android, et plus particulièrement si la nouvelle plateforme avait appris des erreurs et des points faibles de ses prédécesseurs. Bien sûr, « erreurs » et « points faibles » sont souvent des points de vue subjectifs et correspondent surtout à des décisions stratégiques des constructeurs.

Le premier point qui fait parler de lui c'est l'aspect **multi-tâches**. Le système d'exploitation supporte évidement l'exécution de plusieurs tâches simultanées, cependant la plupart des **applications ne pourront pas tourner en tâche de fond**. Il y a des exceptions à ceci—par exemple, on pourra continuer la lecture de musique en tâche de fond avec l'application Zune—et être catégorique sur l'impossibilité de faire tourner un tâche de fond est une généralisation un peu exagérée de toutes manières.

Une application qui ne peut plus s'exécuter au premier plan, parce qu'une notification a été reçue, il y a un appel entrant ou parce que l'utilisateur à choisi de revenir à l'écran de démarrage, par exemple, ne sera pas tout simplement arrêtée. Dans un premier temps, le système d'exploitation demandera à l'application de se mettre en pause, l'application pourra aussi sauvegarder son état dans une sorte de _cookie_ et ce n'est que si système a besoin des ressources utilisées par l'application, qu'il arrêtera cette dernière. Tout ceci est toujours transparent pour l'utilisateur, pour qui l'expérience de changement de contexte devrait être très fluide. On abordera ces aspects plus en détail dans un billet ultérieur.

Une alternative proposée aux tâches de fond c'est le **système de notifications**. Microsoft proposera un service de notifications « _push_ » via sa plateforme Live. Ces notifications pourront alimenter les _tuiles_ de la page de démarrage ou afficher des _toast_ (comme le font certaines applications de messagerie instantanée sur PC) en haut de l'écran, **même si l'application n'est pas démarrée**. Les notifications peuvent aussi être envoyées à une application ouverte pour mettre à jour son état. Le principal avantage du système de notifications est d'exporter la puissance de calcul, et donc la consommation d'énergie, vers Internet ; vers le _cloud_ si vous préférez.

L'autre point qui a enflammé la presse et les blogs c'est **l'absence de presse-papiers ou copier/coller**. C'est un point qui a été souvent critiqué, notamment par la communauté Windows Mobile, sur les premières versions de l'iPhone. Bien que Microsoft n'écarte pas la possibilité de voir cette fonctionnalité apparaître dans une prochaine version de la plateforme, il est clair que ce ne sera pas disponible au début. Par contre, cela ne veut pas dire que les applications ne pourront pas communiquer entre elles. Il est possible d'envoyer des informations aux applications intégrées pour, par exemple, envoyer un mail, prendre une photo, appeler un numéro, enregistrer un contact, …

**Que peut-on faire aujourd'hui ? Quand est-ce que ce sera disponible ?**

Aujourd'hui, Microsoft a mis à disposition **gratuitement** sur Internet l'ensemble des [outils nécessaires au développement d'applications](http://developer.windowsphone.com/windows-phone-7-series/), y compris une version de Visual Studio 2010, Expression Blend et un émulateur. Il y a de plus en plus de ressources pour apprendre à développer pour la plateforme aussi. Mon prochain billet sur Windows Phone 7 abordera ce dont vous avez besoin pour écrire des applications et des jeux pour des téléphones sous Windows Phone 7.

Selon les annonces faites en février, les premiers terminaux sous Windows Phone 7 devraient être disponibles avant la période des fêtes 2010. Une date précise n'a pas été communiquée.

**Conclusion**

Après avoir été largement dépassé par ses compétiteurs dans le domaine de la téléphonie mobile, Microsoft revient en force avec un système d'exploitation, mais surtout avec toute une plateforme qui le place immédiatement aux côtés des principaux acteurs d'aujourd'hui. Malheureusement, Windows Phone 7 n'est pas encore disponible et il est impossible de savoir si le système sera toujours aussi bien placé vis-à-vis des systèmes concurrents lors de sa sortie. Dans tous les cas, il est clair que la création de ce nouveau concept est le fruit de beaucoup d'heures de réflexion pas des experts en expérience utilisateur, mais aussi en développement. En effet, même si la plateforme a été conçue avec l'utilisateur final au centre, la richesse de l'environnement de développement d'applications fait pâlir les alternatives disponibles sur le marché.

Windows Phone 7 n'est pas encore fini et, comme d'habitude, Microsoft a mis à disposition de ses clients un avant-goût de ce que sera cette nouvelle plateforme afin de recueillir le plus de retours possible. Espérons que cette période d'essai sera fructueuse aussi bien pour le constructeur de Redmond que pour nous, les développeurs, afin de permettre à Windows Phone 7, lors de sa sortie, d'être un acteur majeur dans le marché des smartphones.

Entre temps, je vais m'efforcer de découvrir cette nouvelle plateforme—bien que je préfère la considérer plutôt comme un nouveau terrain de jeu—et je me ferai un plaisir de partager avec vous mes découvertes. Pour cela, plusieurs adresses :

*   Mon [blog](http://blog.madd0.com/), que vous lisez en ce moment, mais surtout [son flux RSS](http://feeds.feedburner.com/madd0)
*   Mon [twitter](http://twitter.com/madd0), et notamment [les hashtags #wp7 et #wp7dev](http://search.twitter.com/search?q=&ands=&phrase=&ors=&nots=&tag=wp7+OR+wp7dev&lang=all&from=madd0&to=&ref=&near=&within=15&units=mi&since=&until=&rpp=15)
*   Mon [delicious](http://delicious.com/madd0), et notamment [les tags wp7 et wp7dev](http://delicious.com/madd0/wp7+wp7dev)

N'hésitez pas à me contacter (via commentaire, Twitter, Facebook, formulaire de contact, etc.) si vous avez des questions particulières que vous aimeriez que j'aborde ici.