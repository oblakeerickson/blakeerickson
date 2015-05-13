---
layout: post
title: A Simple Todo App - Part 2
---

In part1 we built the backend for our todo app and now we are going to build the frontend in Angular. Let's get that setup.

The first thing we need to is download angular and add it to our C# project. Go to https://code.angularjs.org and click on 1.2.2 (yes, I'm using an older version). Download angular.js and angular-route.js and put it into your Scripts folder. You now need to show all files and then select each of the files and click add to project.

Now open up BundleConfig.cs located inside of the App_Start folder. At the bottom of the RegisterBundles method add another bundle that we will call "angular".

{% highlight csharp %}
bundles.Add(new ScriptBundle("~/bundles/angular").Include(
    "~/Scripts/angular.js",
    "~/Scripts/angular-route.js"));
{% endhighlight %}

Now that we have angular installed we need a place to store the actually javascript application code. Inside of the Scripts folder create a folder called 'app' and create a file inside of that folder called app.js.

Now we need to go back to our BundleConfig.js file and add another bundle we will call "app".

{% highlight csharp %}
bundles.Add(new ScriptBundle("~/bundles/app").Include(
    "~/Scripts/app/app.js"));
{% endhighlight %}

We still are not quite setup yet we still need to include our bundle into our layout file. So open up _Layout.cshtml which is inside of 'Views/Shared/'. Near the top inside of the `<head></head>` tags add the following lines below the other `@Scripts.Render` line:

{% highlight csharp %}
@Scripts.Render("~/bundles/angular")
@Scripts.Render("~/bundles/app")
{% endhighlight %}

Now open up `Views/Home/Index.cshtml` and replace the entire contents with:

{% highlight html %}
<div ng-view></div>
{% endhighlight %}

In order for Angular to work we need to specify on our `<html>` tag that we are using Angular. Modify this tag so that it looks like:

{% highlight html %}
<html ng-app="app">
{% endhighlight %}
