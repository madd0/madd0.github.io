---
title: 'No siempre se puede ser tan optimista'
date: Sun, 15 Jul 2007 11:24:33 +0000
draft: false
tags: ['.NET', 'C#', 'Español', 'LINQ', 'Technology']
---

Estoy hablando de la concurrencia optimista (optimistic concurrency) por supuesto.

Como ya lo he dicho, mi blog ahora funciona con un nuevo motor. Para no cansarlos con el cuento, perdí mi blog, quería jugar con las últimas tecnologías de Microsoft, así que recuperé el motor de mi amigo [Patrice](http://www.patricelamarche.net/) que utiliza ASP.NET, C# 3.0  y LINQ (y una pizca de ASP.NET AJAX aquí y allá). ¡Y es genial! No solo eso, sinon que también tengo material para el blog.

Así que, por qué voy a comenzar? Si la "concurrencia optimista" y el parráfo de arriba no les a dado pistas, voy a habler de LINQ. LINQ to SQL para ser exactos, o DLINQ, como quieran llamarle.

Empecemos desde el principio. ¿Qué es LINQ?

LINQ, un nombre código que quiere decir _Language Integrated Queries_ (consultas integradas al lenguage), es un conjunto de extensiones de C# y Visual Basic que les da a estos lenguajes una sintaxis nativa para realizar consultas. ¿Consultas de qué? Bueno, por el momento, puede ser cualquier cosa desde objetos (LINQ to Object), XML (LINQ to XML) hasta bases de datos (LINQ to SQL y LINQ to Entities).

¿Y de qué tiene cara? He aquí un ejemplo en C#:

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
```Aunque no lo crean, el código de arriba _es_ C#. ¿Y qué estoy haciendo? Bueno, no voy a entrar en detalles, pero estoy consultando la base de datos para recuperar los posts del blog. La consulta se guarda en una variable de tipo implícito, determinado a partir del resultado de la operación a la derecha de la asignación y los resultados serán objetos de un tipo anónimo que tendrá las propiedades entre llaves. Como lo que estoy usando es DLINQ, el código de arriba será convertido en SQL para ejecutarlo en SQL Server (sí, este es el único servidor soportado actualmente).

¿Y qué es esto de "concurrencia optimista"? ¿Qué es y para qué sirve?

La concurrencia optimista es un modelo de actualización de bases de datos en entornos multiusuarios. Básicamente consiste en comparar una o más columnas del registro a actualizar para verificar que no ha sido modificado por alguien más desde la última vez que se accedió. Este es un método perfectamente válido que se usa en ADO.NET y LINQ.

Entonces, ¿cuál es el problema?

El código arriba funciona con clases creadas por le designer LINQ que viene con Visual Studio Orcas, o debería decir 2008. Y el código funciona muy bien para recuperar todos los posts de la base, pero los problemas comienzan cuando se actualiza un registro:

```
var query = from p in db.Posts
            where p.id\_post == int.Parse(postid)
            select p;

Post originalPost = query.FirstOrDefault();

originalPost.title\_post = newPost.title;
originalPost.text\_post = newPost.description;

db.SubmitChanges();
El error que obtenía era "SQL Server does not handle comparison of NText, Text, Xml or Image data types" (SQL Server no soporta la comparación de typos NText, Text, Xml o Image) y no entedía por qué.

Del mensaje arriba podía adivinar que el problema venía de la consulta generada que comparaba todos los campos de mi tabla antes de actualizarla por la concurrencia optimista. Sin embargo, si ven lo que dice el designer, este no debería ser el caso, o por lo menos no para la única columna NText:

[![dlinq_designer_update_check](http://blog.madd0.com/images/WindowsLiveWriter/lang_enYoucannotalwaysbethatoptimisticla_9832/dlinq_designer_update_check_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enYoucannotalwaysbethatoptimisticla_9832/dlinq_designer_update_check.png)

Ah, pero ¿qué encontramos en el código generado?

```
\[global::System.Data.Linq.Column(Storage="\_text\_post", Name="text\_post",
    DBType="NText NOT NULL", CanBeNull=false)\]
public string text\_post {
    // ...
}
```
En realidad, el problema no viene de lo que se encuentra, pero más bien de lo que falta: falta un atributo de la propiedad:
```
\[global::System.Data.Linq.Column(Storage="\_text\_post", Name="text\_post",
    DBType="NText NOT NULL", CanBeNull=false,
    UpdateCheck=System.Data.Linq.UpdateCheck.Never
)\]
public string text\_post {
    // ...
}
```
Ahora la columna NText no sera comparada y LINQ va a generar la consulta apropiada.


```