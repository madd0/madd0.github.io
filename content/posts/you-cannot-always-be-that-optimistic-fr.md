---
title: 'On ne peut pas toujours être aussi optimiste'
date: Sun, 15 Jul 2007 11:24:06 +0000
draft: false
tags: ['.NET', 'C#', 'Français', 'LINQ', 'Technology']
---

Je parle de l'accès simultané optimiste (optimistic concurrency) bien sûr.

Comme je l'ai déjà dit, mon blog marche maintenant avec un nouveau moteur. Pour résumer, j'ai perdu mon ancien blog, je voulais jouer avec les dernières technologies Microsoft, donc j'ai repris le moteur sur lequel travaille mon ami [Patrice](http://www.patricelamarche.net/) et qui utilise ASP.NET, C# 3.0 et LINQ (et un tout petit peu d'ASP.NET AJAX par ci et par là). Et c'est génial ! Et en plus, j'ai maintenant du matériel pour blogguer.

Alors, par où vais-je commencer ? Si "l'accès simultané optimiste" et le paragraphe ci-dessus ne vous ont pas donné d'indice, je vais parler de LINQ. LINQ to SQL pour être exact, ou DLINQ, peu importe comment on l'appelle.

On va commencer par le début. Qu'est-ce que LINQ ?

LINQ, un nom de code qui veut dire _Language Integrated Queries_ (requêtes intégrées au langage), est un ensemble d'extensions pour C# et Visual Basic qui donne à ces langages une syntaxe native pour réaliser des requêtes. Des requêtes sur quoi ? Bien, pour le moment, ça peut être tout allant des objets (LINQ to Object), du XML (LINQ to XML) ou des bases de données (LINQ to SQL et LINQ to Entities).

Et à quoi ça ressemble ? Voici un exemple en C# :

```
var query = from p in db.Posts
            orderby p.date\_post descending
            select new {
                       Title = p.title\_post,
                       Description = p.text\_post,
                       Date = p.date\_post,
                       p.url\_post,
                       Tags = p.PostsTags,
                       CommentCount = p.PostsComments.Count };
```Vous n'allez peut-être pas me croire, mais le code ci-dessus est _bien_ du C#. Et qu'est-ce que je fais ? Bon, je ne vais pas rentrer dans les détails, mais que fais des requêtes sur ma base de données pour récupérer des posts du blog. La requête est stockée dans une variable typée implicitement à partir de l'opération à droite de l'assignation et les résultats seront des objets d'un type anonyme qui contiendra les propriétés définies entre accolades. Comme c'est du DLINQ que j'utilise, le code ci-dessus sera converti en SQL pour être exécuté sur SQL Server (oui, c'est le seul serveur supporté actuellement).

Et qu'est-ce qu'il en est de cet "accès simultané optimiste" ? Qu'est-ce que c'est et qu'est-ce que ça fait ?

L'accès simultané optimiste est un modèle utilisé pour la mise à jour de bases de données dans des environnements multi-utilisateurs. En quelques mots, ça consiste à comparer un ou plusieurs champs de l'enregistrement à mettre à jour pour verifier qu'il n'a pas été modifié par quelqu'un d'autre depuis la dernière fois qu'il a été accédé. C'est une approche valide utilisée en ADO.NET et LINQ.

Alors, quel est le problème ?

Le code ci-dessus marche avec les classes créées par le nouveau designer LINQ livré avec Visual Studio Orcas, ou devrais-je dire 2008. Et ce code marche très bien pour récupérer tous les posts de la base, mais les problèmes commencent quand j'essaie de mettre à jour un enregistrement comme ceci :

```
var query = from p in db.Posts
            where p.id\_post == int.Parse(postid)
            select p;

Post originalPost = query.FirstOrDefault();

originalPost.title\_post = newPost.title;
originalPost.text\_post = newPost.description;

db.SubmitChanges();
J'avais l'erreur "SQL Server does not handle comparison of NText, Text, XML, or Image data types" (SQL Server ne supporte pas la comparaison de types NText, Text, XML ou Image) et je ne comprenais pas pourquoi.

D'après le message, je pouvais deviner qu'il y avait un problème avec la requête générée qui doit comparer tous les champs de ma table avant la mise à jour pour un accès simultané optimiste. Toutefois, si l'on regarde ce que dit le designer, ça ne devrait pas être le cas, du moins pas pour la seule colonne NText :

[![dlinq_designer_update_check](http://blog.madd0.com/images/WindowsLiveWriter/lang_enYoucannotalwaysbethatoptimisticla_9832/dlinq_designer_update_check_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enYoucannotalwaysbethatoptimisticla_9832/dlinq_designer_update_check.png)

Ah, mais regardez le code généré et qu'est ce que l'on voit ?

```
\[global::System.Data.Linq.Column(Storage="\_text\_post", Name="text\_post",
    DBType="NText NOT NULL", CanBeNull=false)\]
public string text\_post {
    // ...
}
```
En fait, le problème n'est pas tellement ce que l'on voit, mais ce qui manque : il manque un attribut sur la propriété :
```
\[global::System.Data.Linq.Column(Storage="\_text\_post", Name="text\_post",
    DBType="NText NOT NULL", CanBeNull=false,
    UpdateCheck=System.Data.Linq.UpdateCheck.Never
)\]
public string text\_post {
    // ...
}
```
Maintenant la colonne NText ne sera pas comparée et LINQ générera la bonne requête.


```