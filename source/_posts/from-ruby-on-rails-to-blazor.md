---
title: From Ruby on Rails to Blazor (notes)
date: 2020-06-08 19:32:18
tags:
  - Programming
  - Blazor
---

Today I tried to convert an existing Ruby On Rails application to Blazor. Below are a few notes I took while programming.

<!--more-->

* I can make a lot of progress in a short amount of time.
  * But I'm not sure of the long term development (as in months instead of hours)
* Naming things is harder. I have a component `Shared.BlogPost` and a type `Data.BlogPost`. Three guesses what name I wanted to give the variable inside the Component.
  * I now realize that I haven't seen the term `Component` anywhere in the code.
* Routing is difficult as it is part of the page
  * I assumed I would prefer this, but quite a few times there was some kind of collision.
  * I'm not sure how routing priority is done.
* Why is `@page "/blog/page/{PageId:int}"` allowed but does `@page "/blog/{PageSlug:string}"` cause an error? I can understand the reasoning but it feels like an unneeded exception to the rules.
* The default template includes bootstrap, but none of the javascript.
  * Jury is still out on this one. I don't think JavaScript is evil (good code is good, bad code is bad), but when you are using Bootstrap you expect the inclusion of JavaScript-part of BootStrap instead of having to manualy code it.
  * I also think it is a terrible idea to customize how BootStrap looks.
* I'm not a fan of how to syntax needs to be written. `<BlogPost post="@post"></BlogPost>` feels wierd since I prefer the Angular syntax `<BlogPost [post]="post"></BlogPost>`.
* Not sure what to think about the `@code { /* ... */ }` and how it hides the fact that it contains a class. I'm not a fan of the syntax abundance in C# but this feels like the other extreme.
  * Also Angular, React and Hue have JavaScript as primary language which contain HTML (aka the other way around). So Microsoft is breaking this trend. 
  * For a quick site I also think a better division between code is prefered.

Current opinion: I don't think the Blazor is terrible but I get the impression they went further then they needed. Personally I prefer frameworks that use code-behind (Ruby On Rails, Angular) instead of everything in a single file (like React).