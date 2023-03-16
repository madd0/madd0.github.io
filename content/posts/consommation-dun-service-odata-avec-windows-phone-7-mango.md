---
title: 'Consommation d’un service OData avec Windows Phone 7 “Mango”'
date: Thu, 16 Jun 2011 09:40:00 +0000
draft: false
tags: ['Developer Tools', 'Français', 'OData', 'Software Development', 'Technology', 'Windows Phone 7']
---

Ceci est le quatrième billet d’une série sur Windows Phone 7 dans laquelle je construis une application permettant de surveiller la disponibilité de vélos des stations [Vélib’](http://www.velib.paris.fr/) à Paris. Pour rappel, voici la table de matières:

1.  [Introduction et installation des outils](http://blog.madd0.com/2011/06/13/windows-phone-7-introduction-et-installation-des-outils/ "Windows Phone 7 : Introduction et installation des outils")
2.  [Création d’une application et utilisation du contrôle Bing Maps](http://blog.madd0.com/2011/06/14/cration-dune-application-et-utilisation-du-contrle-bing-maps/ "Création d’une application et utilisation du contrôle Bing Maps")
3.  [Le GPS et les services de géolocalisation](http://blog.madd0.com/2011/06/15/le-gps-et-les-services-de-golocalisation/ "Le GPS et les services de géolocalisation")
4.  **Consommation d’un service OData**
5.  [Ajout de punaises sur une carte Bing Maps](http://blog.madd0.com/2011/06/17/ajout-de-punaises-sur-une-carte-bing-maps/ "Ajout de punaises sur une carte Bing Maps")
6.  [Création de nouvelles pages et navigation](http://blog.madd0.com/2011/06/20/cration-de-nouvelles-pages-et-navigation-sur-windows-phone-7/ "Création de nouvelles pages et navigation sur Windows Phone 7")
7.  Création de vignettes sur la page d’accueil

OData
-----

[![odata](http://madd0.files.wordpress.com/2011/06/odata_thumb.png "odata")](http://madd0.files.wordpress.com/2011/06/odata.png)Maintenant que votre application est capable de localiser le téléphone et de centrer la carte sur sa position, il est temps de rechercher les stations Vélib’ se trouvant à proximité. Pour cela nous allons utiliser un service OData qui expose des informations sur les vélos de la ville de Paris.

_Note : malheureusement, cette pratique n’est pas exactement bien vue par les fournisseurs du service, donc il est possible que dans l’avenir ces instruction ne soient plus valables._

Tout d’abord, qu’est-ce qu’[OData](http://www.odata.org/) ? Il s’agit d’un protocole ouvert pour le partage de données. Il permet d’exposer des jeux de données aux formats [ATOM](http://fr.wikipedia.org/wiki/Atom) (XML) ou [JSON](http://fr.wikipedia.org/wiki/JSON) se basant sur une architecture [REST](http://fr.wikipedia.org/wiki/REST). Je ne rentrerai pas dans les détails, mais je vous laisserai visiter [le site officiel](http://www.odata.org/) si vous voulez en savoir plus.

J’ai choisi une source de données OData parce qu’il s’agit d’un protocole léger et facile à consommer, notamment avec l’inclusion dans les _Windows Phone Developer Tools 7.1_, que je vais continuer à appeler les outils “Mango”, d’un client OData.

Le client OData
---------------

Commençons donc par ajouter une référence au service OData :

[![Add Service Reference](http://madd0.files.wordpress.com/2011/06/add-service-reference_thumb.png "Add Service Reference")](http://madd0.files.wordpress.com/2011/06/add-service-reference.png)

Voilà, c’est fini !

Stations Vélib’ à proximité
---------------------------

Le client en place, il ne reste plus qu’à récupérer les stations Vélib’ à proximité de l’utilisateur.

Si vous regardez la [description du service](http://unvelo.fr/api/v1/$metadata) OData de près :

```
<FunctionImport Name="GetStationsInRectangle" EntitySet="Stations"
                ReturnType="Collection(UnVelo.Station)" m:HttpMethod="GET">
  <Parameter Name="point1" Type="Edm.String" Mode="In" />
  <Parameter Name="point2" Type="Edm.String" Mode="In" />
</FunctionImport>
```Vous remarquerez la présence d’une fonction qui retourne les stations présentes dans un rectangle. Ce rectangle est défini par deux points : le coin nord-ouest et le coin sud-est.

Comme nous souhaitons récupérer la liste de stations lorsque la carte affichée change (déplacement, changement de zoom), vous allez vous abonner à l’évènement **ViewChangeEnd**, qui sera déclenché une fois que le déplacement ou le changement de zoom est fini :

```
<map:Map x:Name="Map"
    CredentialsProvider="{StaticResource BingMapsKey}"
    ZoomBarVisibility="Visible" ZoomLevel="17"
    ViewChangeEnd="OnViewChangeEnd" />
```Dans le gestionnaire de l’évènement, vous allez utiliser un **StationRepository** qui a été créé automatiquement par Visual Studio à l’étape précédente, pour lancer un appel asynchrone sur la fonction **GetStationsInRectangle**.```
private readonly string GetStationsInRectangleTemplate = "GetStationsInRectangle?point1='{0}'&point2='{1}'";

private GeoCoordinateWatcher \_gcw;
private StationRepository \_repository;

public MainPage()
{
    InitializeComponent();

    this.\_gcw = new GeoCoordinateWatcher(GeoPositionAccuracy.High);
    this.\_gcw.MovementThreshold = 20;
    this.\_gcw.PositionChanged += this.OnPositionChanged;

    this.\_repository = new StationRepository(new Uri("http://unvelo.fr/api/v1/"));

    this.Loaded += this.OnPageLoaded;
}

private void OnViewChangeEnd(object sender, MapEventArgs e)
{
    this.\_repository.BeginExecute<Station>(
        new Uri(
            string.Format(GetStationsInRectangleTemplate, Map.BoundingRectangle.Northwest, Map.BoundingRectangle.Southeast),
            UriKind.Relative),
        this.GetStationsInRectangleCallbak,
        null);
}
Le client OData créé par Visual Studio supporte uniquement les appels asynchrones dans le but d’éviter des exécutions d’appels longs sur le thread de l’interface graphique, étant donné que ceci dégraderait l’expérience utilisateur. Vous devrez donc créer une méthode _callback_ qui sera appelée à la fin de l’exécution asynchrone pour traiter le résultat de celle-ci :

```
private void GetStationsInRectangleCallbak(IAsyncResult result)
{
    var stations = this.\_repository.EndExecute<Station>(result);
}
```
Vous pouvez vérifier que des stations sont effectivement retournées grâce au débuggeur de Visual Studio. Demain nous les convertirons en punaises à afficher sur la carte. D’ici là, vous avez des données avec lesquelles vous pouvez vous amuser. Si vous avez un peu d’expérience avec Silverlight ou WPF, n’hésitez pas à essayer d’afficher ces données par binding sur différents contrôles.


```