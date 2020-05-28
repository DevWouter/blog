---
title: How to reduce test duration in an angular project
tags:
  - Angular
  - Programming
  - TDD
date: 2020-05-28 20:43:00
---

For some time, I have been working on an Angular. Most of the code is written in a <abbr title="Test Driven Development">TDD</abbr> style. Which means there are now a lot of tests. Tests that will run every time I make a change. Because of the nature of Angular, it takes about 30 seconds to complete, which for me means that TDD is no longer as effective. So how can we reduce the 30 seconds?

<!-- more -->

When you execute `ng test --watch false` is executed. It will compile all the code, run the tests, provide feedback, and exit. This process from start to finish takes up around 3 minutes now. The 30 seconds I mention are only the "run test" and "provide feedback" part. So what one normally does is run `ng test`. 

The reason why I mention `ng test --watch false` is because I'm also interested in reducing the time it takes to compile on the build server.

Waiting 30 seconds to get the results is too long for me. I don't mind waiting a little bit but TDD only works when you get quick results, which for me means I need it below the 15 seconds mark. So how can we reduce the 30 seconds?

One way would be to use `fdescribe(...)` and `fit(...)` but I need to do undo that every time I want to make a commit. And yes, more than once they did become part of the commit.

Now the Angular.io has some of the best documentation, but the part about [Angular workspace configuration](https://angular.io/guide/workspace-config) could be a little bit better. For example: Explaining the pros and cons.

One such advantage I discovered is that when you split your project, it builds everything when you use `ng serve` but when you run `ng test` it will only run the tests inside the application and not the libraries.

Below you will find a step-by-step example of you could something like that up.

```sh
ng new ang-workspace --createApplication="false"
cd ang-workspace
ng generate application ang-app 
ng generate library ang-lib
```

With the above, we have a workspace with a single application and a single library. But the library is not yet being used. So let's fix that!

```html ang-workspace\projects\ang-app\src\app\app.component.hml
<h1>Hello world</h1>
<lib-ang-lib></lib-ang-lib>
```

Of course, we also need to include the library module in `app.module.ts`.

{% codeblock ang-workspace\projects\ang-app\src\app\app.module.ts lang:cs mark:5,13 %}
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';
import { AngLibModule } from 'ang-lib';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AngLibModule,
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
{% endcodeblock %}

And that's all we need to do.
* When you run `ng serve` it will automatically build the library and serves the website and any change you make in the code (application or library) will cause be visible.
* When you run `ng test` it will only run the tests inside the `ang-app`.
* When you run `ng test ang-lib` it will only run the tests in that library.

Now we can move features to another library and this will reduce the number of tests we need to run. Which in turn makes TDD enjoyable again.
