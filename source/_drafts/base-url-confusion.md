---
title: HttpClient respects relative URL with the baseUrl
tags:
  - Programming
  - C#
---

When using the `HttpClient` in C# I kept calling the wrong url for some reason. I was sure that everything was correct. I had the correct URL but everytime I called `http://example.com/api/my-method` the server would reply with 404. But when I paste the same URL in the browser it would work. So what did I do wrong?

At the end of this post you can find the example code which reproduces the the problem.

The problem is that I assumed that when I set the `BaseAddress` it would simply concat it as a string.
In the bad example I would expect something like `http://example.com/api//my-method` which often has the same result as `http://example.com/api/my-method`. But as you might suspect this is not the case.

What happens is similar in the browser. If you are for example on the page `http://example.com/admin/users/12` and you want to navigate to the admin interface. You can do it in a few ways:

* `<a href="http://example.com/admin">...</a>` - Absolute 
* `<a href="//example.com/admin">...</a>` - Relative to the protocol (http/https)
* `<a href="../..">...</a>` - Relative to current path
* `<a href="/admin">...</a>` - Relative to the root/domain

And if you are under the assumption that `HttpClient` simply concats then you are making the same mistake I did. `HttpClient` will respect relative and absolute paths in the same manner as the browser.


```csharp
class Program
{
    static async Task Main(string[] args)
    {
        using var client = new HttpClient();
        client.BaseAddress = new Uri("http://example.com/api/");

        var bad = await client.GetAsync("/my-method");
        var badUrl = bad.RequestMessage.RequestUri;

        var good = await client.GetAsync("my-method");
        var goodUrl = good.RequestMessage.RequestUri;

        // Prints:
        // badUrl:  http://example.com/my-method
        // goodUrl: http://example.com/api/my-method
        Console.WriteLine("badUrl:  " + badUrl);
        Console.WriteLine("goodUrl: " + goodUrl);
    }
}