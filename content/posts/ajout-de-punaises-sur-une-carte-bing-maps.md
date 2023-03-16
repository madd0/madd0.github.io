---
title: 'Ajout de punaises sur une carte Bing Maps'
date: Fri, 17 Jun 2011 09:39:00 +0000
draft: false
tags: ['Bing', 'Developer Tools', 'Français', 'Map', 'Software Development', 'Technology', 'Windows Phone 7']
---

Ceci est le cinquième billet d’une série sur Windows Phone 7 dans laquelle je construis une application permettant de surveiller la disponibilité de vélos des stations [Vélib’](http://www.velib.paris.fr/) à Paris. Pour rappel, voici la table de matières:

1.  [Introduction et installation des outils](http://blog.madd0.com/2011/06/13/windows-phone-7-introduction-et-installation-des-outils/ "Windows Phone 7 : Introduction et installation des outils")
2.  [Création d’une application et utilisation du contrôle Bing Maps](http://blog.madd0.com/2011/06/14/cration-dune-application-et-utilisation-du-contrle-bing-maps/ "Création d’une application et utilisation du contrôle Bing Maps")
3.  [Le GPS et les services de géolocalisation](http://blog.madd0.com/2011/06/15/le-gps-et-les-services-de-golocalisation/ "Le GPS et les services de géolocalisation")
4.  [Consommation d’un service OData](http://blog.madd0.com/2011/06/16/consommation-dun-service-odata-avec-windows-phone-7-mango/ "Consommation d’un service OData avec Windows Phone 7 “Mango”")
5.  **Ajout de punaises sur une carte Bing Maps**
6.  [Création de nouvelles pages et navigation](http://blog.madd0.com/2011/06/20/cration-de-nouvelles-pages-et-navigation-sur-windows-phone-7/ "Création de nouvelles pages et navigation sur Windows Phone 7")
7.  Création de vignettes sur la page d’accueil

On a besoin de punaises
-----------------------

Hier nous nous sommes arrêtés sur une liste stations. Chaque station est représentée par un objet de type `Station` qui contient des propriétés telles que le numéro de station, son adresse, le nombre de vélos et de places disponibles, mais surtout, ses coordonnées géographiques.

La prochaine étape sera donc d’utiliser ces informations pour afficher des punaises sur la carte de la page principale qui donneront un aperçu de l’état de chaque station et qui nous permettront d’accéder à la page de détails de celles-ci.

Pour afficher des punaises sur une carte, vous allez utiliser des calques. Ces calques dérivent de `[MapLayer](http://msdn.microsoft.com/library/microsoft.maps.mapcontrol.maplayer.aspx)` et supportent des éléments d’à peu près n’importe quel type:

![custom_pins](http://madd0.files.wordpress.com/2011/06/custom_pins.png "custom_pins")

Dans notre cas, le `[Pushpin](http://msdn.microsoft.com/library/microsoft.maps.mapcontrol.pushpin.aspx)` fourni dans l’assembly Bing Maps suffira largement. Ce contrôle possède deux propriétés qui nous intéressent :

[![Taj_Mahal](http://madd0.files.wordpress.com/2011/06/taj_mahal_thumb.png "Taj_Mahal")](http://madd0.files.wordpress.com/2011/06/taj_mahal.png)

*   `Content` : est une propriété héritée de `ContentControl` qui permet à la classe `Pushpin` d’afficher à peu près n’importe quel contenu.
*   `Location` : est de type `[GeoCoordinate](http://msdn.microsoft.com/library/system.device.location.geocoordinate.aspx)` et représente les coordonnées géographiques de la punaise qui serviront à la positionner sur la carte.

```
<map:Pushpin Content="Taj Mahal" Location="27.172222,78.042476" />
```Cependant, notre modèle de données, la `Station`, ne correspond pas tout à fait à ce qui est attendu par la classe `Pushpin`. Avant de continuer, vous aurez donc besoin d’un modèle qui représentera les stations sur la carte. Créez la classe `Pin` dans votre projet :```
public class Pin
{
    public Station Station { get; set; }

    public string Label { get { return this.Station.Number.ToString(); } }

    public GeoCoordinate Location
    {
        get
        {
            return new GeoCoordinate(
                (double)this.Station.Latitude,
                (double)this.Station.Longitude);
        }
    }
}
Transformez maintenant votre collection de `Station`s en une collection de `Pin`s :

```
private void GetStationsInRectangleCallbak(IAsyncResult result)
{
    var stations = this.\_repository.EndExecute<Station>(result);

    var p = from s in stations
            select new Pin { Station = s };

    Dispatcher.BeginInvoke(
        new Action<IEnumerable>((pins) => pinLayer.ItemsSource = pins), p);
}

Et un calque pour afficher le tout
----------------------------------

Dans le code ci-dessus, nous avons transformé les stations et assigné cette nouvelle collection au calque de type `[MapItemsControl](http://msdn.microsoft.com/library/microsoft.maps.mapcontrol.mapitemscontrol.aspx)` qui hébergera les punaises.
```
<map:Map x:Name="Map"
    CredentialsProvider="{StaticResource BingMapsKey}"
    ZoomBarVisibility="Visible" ZoomLevel="16"
    ViewChangeEnd="OnViewChangeEnd">
    <map:MapItemsControl x:Name="pinLayer">
        <map:MapItemsControl.ItemTemplate>
            <DataTemplate>
                <map:Pushpin Location="{Binding Location}"
                             Content="{Binding Label}"
                             Tap="OnStationTap" />
            </DataTemplate>
        </map:MapItemsControl.ItemTemplate>
    </map:MapItemsControl>
</map:Map>
```
`MapItemsControl` qui expose, entre autres, les propriétés `ItemsSource` et `ItemTemplate` qui nous permettent de spécifier les éléments à afficher et le template à utiliser pour leur rendu à l’écran, respectivement. Dans l’exemple ci-dessus, chaque punaise sera représentée par un `Pushpin` dont les propriétés sont liées à celles du modèle créé à l’étape précédente. De plus, la méthode **OnStationTap** sera appelée lorsque l’on appuie sur les repères :
```
private void OnStationTap(object sender, GestureEventArgs e)
{
    var station = ((sender as Pushpin).DataContext as Pin).Station;
}
```
Nous savons que c’est un objet de type `Pushpin` qui appelle la méthode et que son `DataContext` est de type `Pin`. Il ne reste plus qu’à appeler la propriété `Station` de ce dernier type pour obtenir les information de la station que l’utilisateur a choisi.

Lundi nous passerons cette station à une nouvelle page qui sera chargée d’afficher ses détails.


```
```