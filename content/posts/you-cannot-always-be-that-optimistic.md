---
title: 'You cannot always be that optimistic'
date: Sun, 15 Jul 2007 13:58:29 +0000
draft: false
tags: ['.NET', 'C#', 'English', 'LINQ', 'Technology']
---

I'm talking about optimistic concurrency of course.

As I've said before, my blog now runs on a new engine. To make a long story short, I lost my old blog, I wanted to play with the newest Microsoft technologies, so I picked up the engine my friend [Patrice](http://www.patricelamarche.net) is working on that uses ASP.NET, C# 3.0 and LINQ (and a sprinkle of ASP.NET AJAX here and there). And it's great! What's more, I now have material for blogging.

So, what am I going to start with? If "optimistic concurrency" and the paragraph above didn't give you a hint, I'm going to talk about LINQ. LINQ to SQL to be precise, or DLINQ, however you want to call it.

Let's start from the beginning. What is LINQ?

LINQ, a codename that stands for Language Integrated Queries, is a set of extensions for C# and Visual Basic that gives these languages a native syntax to perform queries. What kind of queries? Well, for now, it can be anything from objects (LINQ to Object), XML (LINQ to XML) or databases (LINQ to SQL and LINQ to Entities).

And what does it look like? Here's an example in C#:

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
```Believe it or not, the code above _is_ C#. And what am I doing? Well, I'm not going into detail, but I'm querying my database to retrieve blog posts. The query is stored in a variable of a type inferred from the operation on the right of the assignment and the results are going to be objects of an anonymous type that will contain the properties between brackets. Since this is DLINQ I'm using, the code above is automatically converted into SQL to be executed on SQL Server (yes, this is the only server currently supported.)

And what about this "optimistic concurrency" thing? What is it and what does it do?

Optimistic concurrency is a model used for updating databases in multi-user environments. It basically consists in comparing one or more fields of the record to be updated to verify that it hasn't been modified by somebody else since the last time it was accessed. This is a perfectly valid approach that can be used with ADO.NET and LINQ.

So, what's the problem?

The code above works with classes that were generated with the new LINQ designer that comes with Visual Studio Orcas, or should I say 2008. And this code works well for retrieving all posts in the database, but the problems start when I try to update a record using code like this:

```
var query = from p in db.Posts
            where p.id\_post == int.Parse(postid)
            select p;

Post originalPost = query.FirstOrDefault();

originalPost.title\_post = newPost.title;
originalPost.text\_post = newPost.description;

db.SubmitChanges();
I was getting the error "SQL Server does not handle comparison of NText, Text, Xml, or Image data types" and I couldn't understand why.

From the error message above, I could guess that there was a problem with the generated query that compared all fields in my table before updating for optimistic concurrency. However, if you take a look at what the designer says, this shouldn't be the case, at least not for the only NText column:

[![dlinq_designer_update_check](http://blog.madd0.com/images/WindowsLiveWriter/lang_enYoucannotalwaysbethatoptimisticla_9832/dlinq_designer_update_check_thumb.png)](http://blog.madd0.com/images/WindowsLiveWriter/lang_enYoucannotalwaysbethatoptimisticla_9832/dlinq_designer_update_check.png)

Ah, but take a look at the generated code and what will you find?

```
\[global::System.Data.Linq.Column(Storage="\_text\_post", Name="text\_post",
    DBType="NText NOT NULL", CanBeNull=false)\]
public string text\_post {
    // ...
}
```
Well, it's not what you find that's a problem actually, it's what's missing: we're missing an attribute on the property:
```
\[global::System.Data.Linq.Column(Storage="\_text\_post", Name="text\_post",
    DBType="NText NOT NULL", CanBeNull=false,
    UpdateCheck=System.Data.Linq.UpdateCheck.Never
)\]
public string text\_post {
    // ...
}
```
Now the NText column will not be compared and LINQ will generate a proper query.


```