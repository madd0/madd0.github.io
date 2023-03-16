---
title: 'WP7 Mango : Faut-il faire des mises à jour ? Et que se passe-t-il si je les fais ?'
date: Mon, 22 Aug 2011 14:38:56 +0000
draft: false
tags: ['Français', 'Mango', 'Microsoft', 'Software Development', 'Technology', 'Windows Phone 7']
---

[![mango](http://madd0.files.wordpress.com/2011/08/mango_thumb.jpg "mango")](http://madd0.files.wordpress.com/2011/08/mango.jpg)Pour le grand public ce sera **Windows Phone 7.5**—parce que le marketing l’a décidé ainsi. Pour nous, développeurs, ce que nous connaissons aujourd’hui sous le nom code “Mango” sortira bientôt sous le nom officiel **Windows Phone OS 7.1**—parce que chez Microsoft on sait nommer ses classes et ses méthodes, mais pas ses produits.

Un nouvel OS arrive, mais nous savons bien que Microsoft fait toujours un effort surhumain pour faire en sorte que les vielles applications marchent correctement sur les nouvelles versions de ses systèmes d’exploitation, donc il est pertinent de se poser la question :

**Dois-je mettre à jour mon application 7.0 puisqu’elle marchera automatiquement sous 7.1 ?**

La réponse est un peu dans la question : non, vous n’êtes pas obligés de faire de mise à jour. Enfin, sauf si vous vouliez que **votre application marche mieux** et ce avec seulement une ligne de code (lignes des accolades non comprises) !

Je m’explique. Vous vous souvenez du temps que vous avez passé pour faire en sorte que votre application survive le _tombstoning_ correctement ? Vous devez enregistrer l’état de l’application quand elle est désactivée—peu importe la raison—et le restaurer quand est réactivée—peu importe la raison. Ça rend votre application plus agréable à utiliser, mais vous aurez probablement remarqué que la réactivation peut parfois être longue.

Il se trouve que sous Mango, vos processus ne sont plus systématiquement tués par l’OS et donc l’état n’est plus systématiquement perdu ce qui rend sa restitution à chaque réactivation un peu redondant. Heureusement, nous avons un moyen de déterminer si les données sont toujours là et donc nous ne sommes plus obligés de restaurer l’état de l’application que si c’est absolument nécessaire.

\[code language="csharp" highlight="3"\] private void Application\_Activated(object sender, ActivatedEventArgs e) { if (!e.IsApplicationInstancePreserved) { var state = PhoneApplicationService.Current.State; if (state.ContainsKey("myStateData")) { this.data = (string)state\["myStateData"\]; } } } \[/code\]

La valeur de la propriété `IsApplicationInstancePreserved` sera `true` si l’application, et donc son état, étaient déjà en mémoire. Dans ce cas, il n’y a plus besoin de rien faire, dans le cas contraire on restaure l’état comme on le faisait avant. Et voilà, en une ligne vous avez accéléré le chargement de votre application.

**Et maintenant que vous avez une application Mango, que se passe-t-il sur le Marketplace ?**

Microsoft a veut visiblement limiter la fragmentation et veut pousser les utilisateurs à faire la migration de leur OS donc **une fois que vous avez publié une version Mango de votre application, vous ne pourrez plus mettre à jour la version 7.0 sur le Marketplace**. Bien ? Mal ? Je trouve que c’est une mesure un peu drastique, mais je suis plutôt à faveur.

La dernière version 7.0 de votre application sera toujours disponible—bugs et tout—pour les utilisateurs qui sont toujours sur cette plateforme. Tous ceux qui auront migré ne pourront télécharger que la version Mango.

Les utilisateurs qui avaient déjà installé votre application et qui migrent sous Mango, recevront une notification de mise à jour et pourront installer la nouvelle version de votre application. Ceux qui décident de rester sous 7.0 n’auront pas de mise à jour.

Les métadonnées seront communes aux deux versions de l’application en revanche, y compris les screenshots. Microsoft recommande donc d’être très clairs dans les descriptions des applications et de signaler les fonctionnalités qui ne seront disponibles que sous Mango. Ils suggèrent aussi que vous deveniez _ambassadeur-malgré-vous_ en mettant dans vos descriptions un lien vers [http://wpupgrade.ms/mangome](http://wpupgrade.ms/mangome "http://wpupgrade.ms/mangome") pour inciter les utilisateurs à faire la mise à jour du téléphone. Pour les screenshots, vous êtes encouragés à utiliser un _watermark_ identifiant les images qui montrent des fonctionnalités disponibles “Uniquement sous WP 7.5”.