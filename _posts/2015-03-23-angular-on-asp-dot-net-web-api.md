---
layout: post
title: Angular on ASP.NET Web API
---

My goal for this article is to walk you through building a very basic application that uses Angular on the frontend and ASP.NET Web API on the backend so that you can learn how the two frameworks communicate with one another.

The first thing we are going to do is build out the backend by creating a new C# ASP.NET Web API project, create a TodoItem Model, set up the database with Entity Framework, create a controller.

Once the backend is all setup we will add Angular to our project and get it talking to our backend.

## Setting up our project

Open Visual Studio 2013 and create a new Visual C# Web application using .NET Framework 4.5. Name the app 'TodoApp' and press OK.

Select the Web API template. The MVC and Web API boxes should be checked. On the right side make sure that the Authentication is set to No Authentication. You can go ahead and uncheck "Host in the cloud" because we won't be discussing deploying our app in this article. Click OK.

## Creating the TodoItem Model

To create our TodoItem Model right-click on the Models Folder and go to Add->Class. Label the class TodoItem.

Replace all of the using statements with the following two statements:

{% highlight csharp %}
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
{% endhighlight %}

Now let's add the `Id` and `Name` attributes to our class:

{% highlight csharp %}
public class TodoItem
{
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }
}
{% endhighlight %}
