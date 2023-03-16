---
title: 'Création d’une application et utilisation du contrôle Bing Maps'
date: Tue, 14 Jun 2011 09:31:00 +0000
draft: false
tags: ['Bing', 'Developer Tools', 'Français', 'Map', 'Software Development', 'Technology', 'Windows Phone 7']
---

Ceci est le deuxième billet d’une série sur Windows Phone 7 dans laquelle je construis une application permettant de surveiller la disponibilité de vélos des stations [Vélib’](http://www.velib.paris.fr/) à Paris. Pour rappel, voici la table de matières:

1.  [Introduction et installation des outils](http://blog.madd0.com/2011/06/13/windows-phone-7-introduction-et-installation-des-outils/ "Windows Phone 7 : Introduction et installation des outils")
2.  **Création d’une application et utilisation du contrôle Bing Maps**
3.  [Le GPS et les services de géolocalisation](http://blog.madd0.com/2011/06/15/le-gps-et-les-services-de-golocalisation/ "Le GPS et les services de géolocalisation")
4.  [Consommation d’un service OData](http://blog.madd0.com/2011/06/16/consommation-dun-service-odata-avec-windows-phone-7-mango/ "Consommation d’un service OData avec Windows Phone 7 “Mango”")
5.  [Ajout de punaises sur une carte Bing Maps](http://blog.madd0.com/2011/06/17/ajout-de-punaises-sur-une-carte-bing-maps/ "Ajout de punaises sur une carte Bing Maps")
6.  [Création de nouvelles pages et navigation](http://blog.madd0.com/2011/06/20/cration-de-nouvelles-pages-et-navigation-sur-windows-phone-7/ "Création de nouvelles pages et navigation sur Windows Phone 7")
7.  Création de vignettes sur la page d’accueil

Description de l’application
----------------------------

Hier, pressé de vous faire installer les outils, j’ai oublié de vous présenter l’application elle-même !

Il s’agit d’une application très simple, permettant de surveiller la disponibilité des [Vélib’s](http://www.velib.paris.fr/) à Paris. Pour ceux qui ne connaissent pas Vélib’, il s’agit d’un réseau de stations, permettant la location de courte durée de vélos dans la capitale.

Notre application aura donc deux écrans :

[![Screenshot 1](http://madd0.files.wordpress.com/2011/06/screenshot-1_thumb.png "Screenshot 1")](http://madd0.files.wordpress.com/2011/06/screenshot-1.png)[![Screenshot 2](http://madd0.files.wordpress.com/2011/06/screenshot-2_thumb.png "Screenshot 2")](http://madd0.files.wordpress.com/2011/06/screenshot-2.png)

Le premier permet d’apercevoir, sur une carte qui occupe l’écran entier, les stations à proximité de l’utilisateur. Le deuxième sera accessible lorsque l’on appuie sur une station sur la carte ou depuis l’écran d’accueil.

Création du projet
------------------

Nous allons commencer par créer un nouveau projet.

[![New Project](http://madd0.files.wordpress.com/2011/06/new-project_thumb.png "New Project")](http://madd0.files.wordpress.com/2011/06/new-project.png)

Sélectionnez un projet de type _Windows Phone Application_ dans la catégorie _Silverlight for Windows Phone_. J’ai appelé mon projet **UnVelo.Wp7**, mais vous êtes libres d’appeler le vôtre comme vous le souhaitez.

Comme j’avais prévenu, j’aurai besoin de fonctionnalités disponibles uniquement dans la nouvelle version du système d’exploitation. Choisissez donc les outils “Mango” ou _Windows Phone 7.1_ :

[![New Windows Phone Application](http://madd0.files.wordpress.com/2011/06/new-windows-phone-application_thumb.png "New Windows Phone Application")](http://madd0.files.wordpress.com/2011/06/new-windows-phone-application.png)

[![WindowClipping](http://madd0.files.wordpress.com/2011/06/windowclipping_thumb.png "WindowClipping")](http://madd0.files.wordpress.com/2011/06/windowclipping.png) Votre nouveau projet contient déjà un certain nombre de fichiers :

*   _App.xaml_ et _App.xaml.cs_ contiennent du code relatif à l’application dans sa globalité, par exemple, des gestionnaires d’évènements ou, dans quelques instants, des ressources globales.
*   _ApplicationIcon.jpg_, _Background.jpg_ et _SplashScreenImage.jpg_ sont des images utilisées par le téléphone pour l’icône de l’application, la vignette de l’écran d’accueil et au démarrage de l’application. Je ne rentrerai pas dans le détail pour le moment, mais je vous encourage à jouer avec pour voir comment elles se comportent.
*   _MainPage.xaml_ a été configurée dans _App.xaml_ comme étant la page de démarrage de notre application, c’est donc ici que nous allons commencer.

[![ViewHolder](http://madd0.files.wordpress.com/2011/06/viewholder_thumb.png "ViewHolder")](http://madd0.files.wordpress.com/2011/06/viewholder.png)

La page contient un certain nombre d’éléments par défaut. Ceux-ci permettent au développeur d’indiquer le nom de l’application, le titre de page et, dans une grille appelée _ContentPanel_, d’ajouter le contenu qu’il souhaite. Dans notre cas, cette page ne nous convient pas du tout, nous allons donc tout supprimer et ajouter notre plan.

Le contrôle Bing Maps
---------------------

Pour ajouter un plan dans la page principale, nous allons utiliser le contrôle Bing Maps pour Silverlight fourni avec Windows Phone. Pour cela, vous devez ajouter une référence vers l’assembly _Microsoft.Phone.Controls.Maps_ :

[![Add Reference](http://madd0.files.wordpress.com/2011/06/add-reference_thumb.png "Add Reference")](http://madd0.files.wordpress.com/2011/06/add-reference.png)

Ensuite, pour utiliser le contrôle dans le code XAML, il faut donner un alias au namespace _Microsoft.Phone.Controls.Maps_ dans le fichier _MainPage.xaml_ :

```
<phone:PhoneApplicationPage
    x:Class="UnVelo.Wp7.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:phone="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone"
    xmlns:shell="clr-namespace:Microsoft.Phone.Shell;assembly=Microsoft.Phone"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:map="clr-namespace:Microsoft.Phone.Controls.Maps;assembly=Microsoft.Phone.Controls.Maps"
    mc:Ignorable="d" d:DesignWidth="480" d:DesignHeight="768"
    FontFamily="{StaticResource PhoneFontFamilyNormal}"
    FontSize="{StaticResource PhoneFontSizeNormal}"
    Foreground="{StaticResource PhoneForegroundBrush}"
    SupportedOrientations="Portrait" Orientation="Portrait"
    shell:SystemTray.IsVisible="True">
```Ce qui nous permettra enfin d’ajouter le contrôle à notre page :```
<Grid x:Name="LayoutRoot" Background="Transparent">
    <map:Map />
</Grid>
```Un petit _Ctrl+F5_ compilera et lancera l’émulateur pour que nous puissions enfin voir notre application pour la première fois :

[![Windows Phone Emulator](http://madd0.files.wordpress.com/2011/06/windows-phone-emulator_thumb.png "Windows Phone Emulator")](http://madd0.files.wordpress.com/2011/06/windows-phone-emulator.png)

En l’état, vous ne pouvez pas faire grand-chose avec l’application. Vous pouvez tout de même utiliser un doigt pour déplacer la carte, faire un “double-clic” en appuyant deux fois rapidement pour zoomer et quitter l’application à l’aide du bouton Précédent de l’émulateur. Si vous avez un écran tactile, vous pourrez aussi tester des gestes comme le “pincement” pour zoomer.

Vous avez surement remarquée aussi la présence d’un message au milieu du contrôle, vous indiquant que vous n’avez pas fourni d’information d’identification et vous invitant à créer un compte développeur.

Ce compte peut être créé gratuitement sur le site [Bing Maps Account Center](http://www.bingmapsportal.com/) et sera lié à un Live Id. Sur ce site vous pourrez créer une nouvelle “clé” pour l’utilisation des APIs Bing Maps.

Vous pouvez créer une clé de type “Développeur” ou “Mobile”. Les deux sont gratuites et vous permettront de travailler sans problème sur votre application Windows Phone 7. Une clé “Mobile” sera nécessaire lors du déploiement d’une application utilisant le contrôle Bing Maps, en revanche, sinon vous risquez de rencontrer des problèmes dus aux limitations des autres types de clé.

Une fois que vous avez obtenu votre clé, vous allez la copier et en faire une ressource globale de votre application, car vous allez en avoir besoin à plusieurs endroits.

Ouvrez donc le fichier _App.xaml_, dans lequel vous allez ajouter le namespace _Microsoft.Phone.Controls.Maps_, comme vous l’avez fait au-dessus et vous allez ajouter votre clé à la section _Resources_ :

```
<Application.Resources>
    <map:ApplicationIdCredentialsProvider x:Key="BingMapsKey" ApplicationId="\[Votre clé ici\]" />
</Application.Resources>
```Vous pouvez maintenant la référencer depuis _MainPage.xaml_ :```
<map:Map CredentialsProvider="{StaticResource BingMapsKey}"
         ZoomBarVisibility="Visible"
         ZoomLevel="12"
         Center="48.856614,2.352222"/>
```Je m’arrêterai ici pour aujourd’hui. Vous avez tout ce qu’il vous faut pour jouer un peu avec le contrôle Bing Maps. N’hésitez pas à tester différentes propriétés pour changer l’affichage.

Demain nous utiliserons les services de géolocalisation pour centrer la carte sur la position actuelle de l’utilisateur automatiquement.