---
title: HttpClient respects relative URL with the baseUrl
tags:
  - Programming
  - C#
date: 2020-06-09 14:08:01
---


When using the `HttpClient` in C# I kept getting a 404/405. I was certain that everything was correct. The BaseAddress, the URL. I even double checked it my copy-pasting the URL in to the browser. So what went wrong?

At the end of this post you can find the example code which reproduces and demonstrates the the problem.

<!-- more -->

The problem is the assumption that by setting the client uses the `BaseAddress` to concat two values. However the `HttpClient` respects absolute and relative URLs in the same way as your browse does. That means that the `requestUri`-parameter acts in the same manner as the `href` attribute in HTML

* `<a href="http://example.com/admin">...</a>` - Absolute 
* `<a href="//example.com/admin">...</a>` - Relative to the protocol (http/https)
* `<a href="../..">...</a>` - Relative to current path
* `<a href="index.html">...</a>` - Relative to the current path
* `<a href="/admin">...</a>` - Relative to the root/domain

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
```