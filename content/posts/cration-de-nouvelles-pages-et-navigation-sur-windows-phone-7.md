---
title: 'Création de nouvelles pages et navigation sur Windows Phone 7'
date: Mon, 20 Jun 2011 09:51:00 +0000
draft: false
tags: ['Developer Tools', 'Français', 'Software Development', 'Technology', 'Windows Phone 7']
---

Ceci est le sixième billet d’une série sur Windows Phone 7 dans laquelle je construis une application permettant de surveiller la disponibilité de vélos des stations [Vélib’](http://www.velib.paris.fr/) à Paris. Pour rappel, voici la table de matières:

1.  [Introduction et installation des outils](http://blog.madd0.com/2011/06/13/windows-phone-7-introduction-et-installation-des-outils/ "Windows Phone 7 : Introduction et installation des outils")
2.  [Création d’une application et utilisation du contrôle Bing Maps](http://blog.madd0.com/2011/06/14/cration-dune-application-et-utilisation-du-contrle-bing-maps/ "Création d’une application et utilisation du contrôle Bing Maps")
3.  [Le GPS et les services de géolocalisation](http://blog.madd0.com/2011/06/15/le-gps-et-les-services-de-golocalisation/ "Le GPS et les services de géolocalisation")
4.  [Consommation d’un service OData](http://blog.madd0.com/2011/06/16/consommation-dun-service-odata-avec-windows-phone-7-mango/ "Consommation d’un service OData avec Windows Phone 7 “Mango”")
5.  [Ajout de punaises sur une carte Bing Maps](http://blog.madd0.com/2011/06/17/ajout-de-punaises-sur-une-carte-bing-maps/ "Ajout de punaises sur une carte Bing Maps")
6.  **Création de nouvelles pages et navigation**
7.  Création de vignettes sur la page d’accueil

Un modèle de programmation Web
------------------------------

[![Screenshot 2](http://madd0.files.wordpress.com/2011/06/screenshot-2_thumb1.png "Screenshot 2")](http://madd0.files.wordpress.com/2011/06/screenshot-21.png)

Vous avez surement remarqué l’absence de fenêtres dans notre application Windows Phone 7. Cela aurait pu vous marquer, notamment si vous êtes habituées au développement sur environnements _desktop_, voire aussi sur des anciennes versions de Windows Mobile.

Si je devais faire un parallèle entre le développement sur Windows Phone 7 et une autre plateforme, je me verrais obligé de le comparer au développement Web—en tout cas pour ce qui est des applications Silverlight ; les application XNA sont une toute autre histoire.

En effet, si vous examinez le code généré dans le fichier **App.xaml.cs** vous trouverez qu’au démarrage de l’application on commence par déclarer comme élément racine un objet de type `PhoneApplicationFrame`. C’est dans ce _frame_ que vont être affichées par la suite vos pages, qui dérivent de la classe `PhoneApplicationPage`. Le similitudes ne se limitent pas au _frame_ et aux pages. Vous verrez qu’on retrouvera des concepts tels que les URIs, les hyperliens, etc.

Une nouvelle page
-----------------

Hier nous avons permis à l’utilisateur d’afficher des stations sur sa carte. Il est même capable d’appuyer sur l’une de ces dernières et, de notre côté, nous savons identifier la station qu’il a sélectionnée, mais il nous manque quelque chose pour en afficher les détails.

Ajoutez à votre projet un nouvel élément. Sélectionnez une nouvelle _Windows Phone Portrait Page_ parmi les templates _Silverlight for Windows Phone_.

[![Add New Item - UnVelo.Wp7](http://madd0.files.wordpress.com/2011/06/add-new-item-unvelo-wp7_thumb.png "Add New Item - UnVelo.Wp7")](http://madd0.files.wordpress.com/2011/06/add-new-item-unvelo-wp7_.png)

La page créée ressemble à la page principale lorsque nous avons démarré le projet.

Cette fois-ci, nous allons travailler sur le modèle par défaut en remplaçant certaines valeurs et en le complétant avec les contrôles nécessaires pour obtenir un affichage comme celui sur la capture au début de ce billet.

Commençons par modifier la partie du haut :

```
<StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
    <TextBlock x:Name="ApplicationTitle" Text="UN VELO.FR"
               Style="{StaticResource PhoneTextNormalStyle}"/>
    <TextBlock x:Name="PageTitle" Text="{Binding Number, StringFormat='Station {0}'}"
               Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
</StackPanel>
```Le nom de l’application sera une valeur constante, en revanche, le titre devra afficher le numéro de station. Nous utilisons donc une expression de _binding_ pour afficher la propriété `Number` de la classe `Station`. Petite nouveauté “Mango” : comme on utilise enfin Silverlight 4, nous avons accès à la propriété `StringFormat` de l’expression de _binding_, ce qui nous permet de personnaliser un peu le texte affiché sans passer par des convertisseurs ou des piles de `TextBlock`s.

En raison de ce qui semblerait être un bug dans le contrôle Bing Maps, je n’ai pas pu placer tous mes contrôles dans le **ContentPanel** fourni pour cet effet. J’ai donc modifié le **LayoutRoot** :

```
<Grid x:Name="LayoutRoot" Background="Transparent">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="\*"/>
    </Grid.RowDefinitions>

    <Grid.Resources>
        <local:StationConverter x:Key="StationConverter" />
    </Grid.Resources>
<!-- ... -->
En y ajoutant une ligne, j’ai pu placer la carte juste au dessus du **ContentPanel** :

```
<map:Map Margin="12,0,12,0" Grid.Row="1" Grid.ColumnSpan="2" Height="250"
        CredentialsProvider="{StaticResource BingMapsKey}" ZoomLevel="16"
        Center="{Binding Converter={StaticResource StationConverter}}">
    <map:MapItemsControl x:Name="pins"
        ItemsSource="{Binding Converter={StaticResource StationConverter}}">
        <map:MapItemsControl.ItemTemplate>
            <DataTemplate>
                <map:Pushpin Location="{Binding Location}" />
            </DataTemplate>
        </map:MapItemsControl.ItemTemplate>
    </map:MapItemsControl>
</map:Map>

<!--ContentPanel - place additional content here-->
<StackPanel x:Name="ContentPanel" Grid.Row="2" Margin="12,12,12,0">
    <TextBlock Text="{Binding Name}"
               FontFamily="{StaticResource PhoneFontFamilySemiBold}"
               FontSize="{StaticResource PhoneFontSizeLarge}"
               Foreground="{StaticResource PhoneAccentBrush}" />
    <TextBlock Style="{StaticResource PhoneTextLargeStyle}"
      Text="{Binding AvailableBikes, StringFormat='Vélos disponibles : {0}'}" />
    <TextBlock Style="{StaticResource PhoneTextLargeStyle}"
      Text="{Binding FreeSpaces, StringFormat='Places disponibles : {0}'}" />
</StackPanel>
Le code ci-dessus est moins complexe qu’il ne parait. Certes, la présence d’un _converter_ dans les _bindings_ vous perturbe certainement un peu et le rendu fait par le designer est assez décevant :

[![ViewHolder2](http://madd0.files.wordpress.com/2011/06/viewholder2_thumb.png "ViewHolder2")](http://madd0.files.wordpress.com/2011/06/viewholder2.png)

Tous les _bindings_ ont été faits en supposant qu’un objet de type `Station` se trouve dans le `DataContext` de la page. Or nous n’avons pas encore défini de station, donc rien ne s’affiche.

On a besoin d’une station !

Naviguer entre les pages
------------------------

Revenons sur la page principale ; plus spécifiquement, dans le gestionnaire de l’évènement `Tap` des punaises :
```
private void OnStationTap(object sender, GestureEventArgs e)
{
    var station = (sender as Pushpin).DataContext;
}
```
Nous avons une station dont nous voulons afficher les détails.

Pas question ici de créer une nouvelle instance de la classe que nous venons de créer. Je vous rappelle que nous sommes dans un modèle type Web et nous allons tout simplement naviguer entre les pages comme nous l’aurions fait avec des documents HTML.

Pour cela, nous avons à notre disposition un `[NavigationService](http://msdn.microsoft.com/library/system.windows.navigation.navigationservice(v=VS.92).aspx)` qui est accessible par la propriété homonyme de vos pages. Ce service propose une méthode `Navigate` qui prend en paramètre un URI relatif vers la destination :

```
private void OnStationTap(object sender, GestureEventArgs e)
{
    var station = (sender as Pushpin).DataContext;

    NavigationService.Navigate(new Uri("/DetailsPage.xaml", UriKind.Relative));

    // Dans la version ci-dessous on spécifie l'assembly (UnVelo.Wp7)
    // Cela peut-être utile si vos pages se trouvent dans un assembly
    // différent de celui en cours d'exécution
    // NavigationService.Navigate(new Uri("/UnVelo.Wp7;component/DetailsPage.xaml", UriKind.Relative));
}
Le code ci-dessus (les deux versions) produit l’effet désiré : le téléphone change de page et affiche celle que nous avons préparée plus haut. De plus, la page principale a été placée sur la pile de navigation, ce qui nous permet d’y retourner via le bouton **Précédent**.

En revanche, le code ne fait que ça : passer la page ; et comme nous n’instancions pas la page nous-mêmes, il n’y a, a priori pas de moyen de passer des données via des propriétés de la page comme on a l’habitude de le faire sous d’autres plateformes.

Transmission de données entre les pages
---------------------------------------

Il y a deux manières de passer des données en mémoire d’une page à une autre : la _query string_ (comme dans le Web) et l’état courant du `PhoneApplicationService`.

Comme dans une page web, on peut passer des informations dans l’URI de la page appelée, par exemple, dans la page principale on écrit :

```
private void OnStationTap(object sender, GestureEventArgs e)
{
    var pin = ((sender as Pushpin).DataContext as Pin);

    var uri = string.Format("/DetailsPage.xaml?id={0}", pin.Station.Number);
    NavigationService.Navigate(new Uri(uri, UriKind.Relative));
}
Et dans la page détails on peut récupérer la valeur avec le code suivant :

```
public override void OnNavigatedTo(NavigationEventArgs e)
{
    var number = NavigationContext.QueryString\["id"\];

    // ...

    base.OnNavigatedTo(e);
}
La méthode **OnNavigatedTo** de la page est appelée lorsque l’on arrive sur une page—son opposé est **OnNavigatedFrom**, qui est appelée juste avant que l’on quitte une page. Dans cette méthode on pourrait récupérer les différentes valeurs qui ont été passées dans la _query string_ pour les assigner aux contrôles de la page ou pour effectuer des _data bindings_.

Toutefois, dans l’exemple qui nous concerne, nous voulons passer bien plus d’informations que juste le numéro de station, et nous avons toutes ces informations encapsulées dans une instance de la classe `Station`. De plus, il peut exister des cas où les données qui doivent être partagées entre les pages ne peuvent pas être transformées en chaine de caractères pour être concaténées à l’URI de la page. Pour ces cas-là, la classe `PhoneApplicationService` mantient un état courant dans lequel on peut stocker des objets pour les partager entre plusieurs pages :

```
private void OnStationTap(object sender, GestureEventArgs e)
{
    var pin = ((sender as Pushpin).DataContext as Pin);

    PhoneApplicationService.Current.State\["currentStation"\] = pin.Station;

    NavigationService.Navigate(new Uri("/DetailsPage.xaml", UriKind.Relative));
}
Les lignes ci-dessus enregistrent dans un emplacement de l’état courant de l’application, que l’on appelle arbitrairement _currentStation_, la station contenue dans le DataContext de la punaise qui a été appuyée par l’utilisateur. Du côté de la page de détails, quelques lignes suffiront à récupérer cet objet pour afficher les informations qu’il contient :

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    object station;

    if (PhoneApplicationService.Current.State.TryGetValue("currentStation", out station))
    {
        this.DataContext = station;
    }

    base.OnNavigatedTo(e);
}
On aurait pu se contenter de faire tout simplement l’assignation :

```
this.DataContext = PhoneApplicationService.Current.State\["currentStation"\];
```
Mais l’utilisation de la méthode **TryGetValue** maintenant nous permettra de prévoir des cas où il n’y a pas de valeur pour la clé _currentStation_ à l’avenir.

Grâce aux bindings que nous avions déclarés lorsque nous avons créé la page de détails, le fait d’assigner un objet de type **Station** à son DataContext suffit à afficher la page comme on le voulait.

[![Details_page](http://madd0.files.wordpress.com/2011/06/details_page_thumb.png "Details_page")](http://madd0.files.wordpress.com/2011/06/details_page.png)

Si vous essayez d’exécuter le code il vous manquera cependant la classe **StationConverter** que nous avons utilisée pour simplifier certains bindings :

```
public class StationConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        var station = value as Station;

        if (null == station)
        {
            return value;
        }

        if (typeof(GeoCoordinate) == targetType)
        {
            return new GeoCoordinate((double)station.Latitude, (double)station.Longitude);
        }
        else if (typeof(IEnumerable) == targetType)
        {
            return new object\[\] { new Pin { Station = station } }.AsEnumerable();
        }

        return value;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
Nous approchons de la fin de la série. Maintenant que nous avons réussi à afficher les détails d’une station dans une page, nous allons profiter d’une des nouveautés de “Mango” qui nous permettra de modifier, à partir du code uniquement, des vignettes sur la page d’accueil pour y afficher, par exemple, le nombre de vélos disponibles dans une station. Mais ce code-là, on le verra demain.


```
```
```
```
```
```
```
```