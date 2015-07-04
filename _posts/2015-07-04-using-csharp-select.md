---
layout: post
title: Using C# Select
summary: > 
        The other day I was using Underscore quite a bit while working on some
        Angular code. There are many helpful features like map, filter,
        and range. I then needed to do some C# changes on the server side and
        realized that C# has similar helpful features like Underscore does for working
        with collections of data. These helpful features are available because of
        LINQ.
tags: csharp
---

The other day I was using [Underscore][1] quite a bit while working on some
[Angular][2] code. There are many helpful features like [`map`][3], [`filter`][4],
and [`range`][5]. I then needed to do some C# changes on the server side and
realized that C# has similar helpful features like Underscore does for working
with collections of data. These helpful features are available because of
[LINQ][6].

Here is an example of how to use the [.Select method][7] on a collection in C#. What
we can do is take a list of employees in a single company and iterate through
them using the .Select method to return a list of their email addresses. First
let's make a list of employees:

{% highlight csharp %}
var employees = new List<string>();
employees.Add("steve");
employees.Add("bob");
employees.Add("amy");
{% endhighlight %}

Now we can do some magic to return a list of emails using the `.Select` method:

{% highlight csharp %}
var emails = employees.Select(x => x + "@example.com");
{% endhighlight %}

Now that we have our email list we can print them out to the console (or send
emails, add them to a database table, etc.):

{% highlight csharp %}
foreach (var email in emails)
{
    Console.WriteLine(email);
}
{% endhighlight %}

Below is the entire source for the Console Application we just built:

{% highlight csharp %}
using System;
using System.Collections.Generic;
using System.Linq;

namespace Select
{
    class Program
    {
        static void Main(string[] args)
        {
            var employees = new List<string>();
            employees.Add("steve");
            employees.Add("bob");
            employees.Add("jon");

            var emails = employees.Select(x => x + "@example.com");
            
            foreach (var email in emails)
            {
                Console.WriteLine(email);
            }
        }
    }
}
{% endhighlight %}

[1]: http://underscorejs.org/
[2]: https://angularjs.org/
[3]: http://underscorejs.org/#map
[4]: http://underscorejs.org/#filter
[5]: http://underscorejs.org/#range
[6]: https://msdn.microsoft.com/en-us/library/vstudio/system.linq(v=vs.100).aspx
[7]: https://msdn.microsoft.com/en-us/library/vstudio/bb548891(v=vs.100).aspx?cs-save-lang=1&cs-lang=csharp#code-snippet-1
