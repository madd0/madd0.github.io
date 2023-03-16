---
title: 'Le GPS et les services de géolocalisation'
date: Wed, 15 Jun 2011 09:40:00 +0000
draft: false
tags: ['Developer Tools', 'Français', 'Geolocalisation', 'GPS', 'Software Development', 'Technology', 'Windows Phone 7']
---

Ceci est le troisème billet d’une série sur Windows Phone 7 dans laquelle je construis une application permettant de surveiller la disponibilité de vélos des stations [Vélib’](http://www.velib.paris.fr/) à Paris. Pour rappel, voici la table de matières:

1.  [Introduction et installation des outils](http://blog.madd0.com/2011/06/13/windows-phone-7-introduction-et-installation-des-outils/ "Windows Phone 7 : Introduction et installation des outils")
2.  [Création d’une application et utilisation du contrôle Bing Maps](http://blog.madd0.com/2011/06/14/cration-dune-application-et-utilisation-du-contrle-bing-maps/ "Création d’une application et utilisation du contrôle Bing Maps")
3.  **Le GPS et les services de géolocalisation**
4.  [Consommation d’un service OData](http://blog.madd0.com/2011/06/16/consommation-dun-service-odata-avec-windows-phone-7-mango/ "Consommation d’un service OData avec Windows Phone 7 “Mango”")
5.  [Ajout de punaises sur une carte Bing Maps](http://blog.madd0.com/2011/06/17/ajout-de-punaises-sur-une-carte-bing-maps/ "Ajout de punaises sur une carte Bing Maps")
6.  [Création de nouvelles pages et navigation](http://blog.madd0.com/2011/06/20/cration-de-nouvelles-pages-et-navigation-sur-windows-phone-7/ "Création de nouvelles pages et navigation sur Windows Phone 7")
7.  Création de vignettes sur la page d’accueil

Accéder à la position actuelle du téléphone
-------------------------------------------

On voudrait, lorsque l’application se lance et lorsque l’utilisateur bouge, que la carte que nous avons ajoutée hier soit centrée sur leur position courante. Pour cela nous allons utiliser des classes du namespace [System.Device.Location](http://msdn.microsoft.com/library/ee426011.aspx) et, plus spécifiquement, la classe [GeoCoordinateWatcher](http://msdn.microsoft.com/library/system.device.location.geocoordinatewatcher.aspx).

Cette classe nous permet d’obtenir la position du téléphone en utilisant plusieurs sources : les bornes WiFi à proximité, les tours cellulaires et, bien sûr, le GPS. C’est pour cette raison que dans le titre du billet je parle de GPS _et_ des services de géolocalisation.

Pour lancer la détection de la position courante de l’utilisateur dans notre page principale, nous allons écrire un peu de C#. Ouvrez le fichier _MainPage.xaml.cs_ pour ajouter une instance de GeoCoordinateWatcher à votre page :

```
private GeoCoordinateWatcher \_gcw;

// Constructor
public MainPage()
{
    InitializeComponent();

    this.\_gcw = new GeoCoordinateWatcher(GeoPositionAccuracy.High);
    this.\_gcw.MovementThreshold = 20;
    this.\_gcw.PositionChanged += this.OnPositionChanged;

    this.Loaded += this.OnPageLoaded;
}
Vous aurez remarqué que je demande au GeoCoordinateWatcher de récupérer la position du téléphone avec le plus de précision possible. Ceci parce que j’ai besoin de lui montrer des information qui sont très liées à sa position exacte. Si mon application avait seulement besoin de connaitre la position approximative de l’utilisateur, j’aurais passé la valeur **GeoPositionAccuracy.Normal** au constructeur, ce qui permet au téléphone de mieux gérer ses ressources. J’ai aussi spécifié la valeur minimale, en mètres, que la position du téléphone doit changer pour qu’un évènement de changement de position soit levé. Ceci évitera que le logiciel rafraichisse inutilement ses données trop souvent.

J’ai attendu que la page soit totalement chargée avant de démarrer le service de localisation :

```
private void OnPageLoaded(object sender, RoutedEventArgs e)
{
    this.\_gcw.Start();
}

void OnPositionChanged(object sender, GeoPositionChangedEventArgs<GeoCoordinate> e)
{
    this.Map.Center = e.Position.Location;
}
Lorsque la position change et que la méthode **OnPositionChanged** est appelée, je récupère la position actuelle et j’en fait le centre de la carte que j’ai ajoutée hier à la page. D’ailleurs, le code du contrôle Bing Maps a changé un peu depuis hier :

```
<map:Map x:Name="Map"
    CredentialsProvider="{StaticResource BingMapsKey}"
    ZoomBarVisibility="Visible" ZoomLevel="17"/>
```

Le simulateur
-------------

Si vous lancez votre application dans l’émulateur, vous constaterez rapidement que son comportement a changé. La carte est désormais automatiquement centrée sur le campus de Microsoft à Redmond :

[![Windows Phone Emulator (3)](http://madd0.files.wordpress.com/2011/06/windows-phone-emulator-3_thumb.png "Windows Phone Emulator (3)")](http://madd0.files.wordpress.com/2011/06/windows-phone-emulator-3.png)

Ceci s’explique par le nouveau simulateur GPS installé avec les outils “Mango”. Pour y accéder, cliquez sur le double chevron dans la boite à outils de l’émulateur, puis sur l’onglet _Location_ de la fenêtre qui s’ouvre.

[![Additional Tools](http://madd0.files.wordpress.com/2011/06/additional-tools_thumb.png "Additional Tools")](http://madd0.files.wordpress.com/2011/06/additional-tools.png)

Tant que le bouton _Live_ de nouvelle fenêtre est activé (gris foncé), chaque clic sur la carte placera une punaise qui deviendra la position actuelle communiqué aux services de géolocalisation du téléphone.

Vous pouvez utiliser la souris pour naviguer sur la carte et les contrôles de zoom pour obtenir plus ou moins de précision. Vote application étant à l’écoute des changements de position des services de géolocalisation, elle devrait centrer la carte sur une nouvelle position à chaque fois que vous cliquez sur la carte du simulateur. Pour préparer l’image ci-dessous, j’ai effectué une recherche avec les mots clés “Paris, France”, j’ai ensuite zoomé sur l’Ile de la Cité et cliqué près de Notre-Dame pour y placer une punaise et centrer le téléphone sur cette nouvelle position.

[![Additional Tools (2)](http://madd0.files.wordpress.com/2011/06/additional-tools-2_thumb.png "Additional Tools (2)")](http://madd0.files.wordpress.com/2011/06/additional-tools-2.png)

Je vous laisse étudier plus en détail les services de géolocalisation et vous amuser avec le simulateur si vous le souhaitez. Vous pouvez essayer de créer des parcours qui simuleront une personne qui se déplace, par exemple.

Demain nous allons chercher les stations Vélib’ qui se trouvent à proximité du téléphone.


```
```