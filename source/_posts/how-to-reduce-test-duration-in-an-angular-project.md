---
title: Reduce test duration in an Angular project
tags:
  - Angular
  - Programming
  - TDD
date: 2020-05-28 20:43:00
---

For some time, I have been working on an Angular project. Most of the code is written in a <abbr title="Test Driven Development">TDD</abbr> style. Which means there are a lot of tests. Tests that will run every time I make a change. Because of the nature of Angular, it takes about 30 seconds to complete, which for me means that TDD start losing it's effectiveness. So how can we reduce the 30 seconds delay?

<!-- more -->

When you execute `ng test` it will compile all the code, run the tests, provide feedback, and exit. This process from start to finish takes around 3 minutes for me right now. The 30 seconds mentioned earlier is only the "run test" and "provide feedback" part. 

Waiting 30 seconds for the results is too long for me. I don't mind waiting a little bit but TDD only works when you get quick results, which for me means it needs to be below the 15 seconds. So how can we reduce it to 15 seconds?

One way would be to use `fdescribe(...)` and `fit(...)` but then I need to do undo that every time I commit. And experience has thought me that it was too easy to forget. Resulting in the build server only running a few of the tests instead of all.

Angular.io has great documentation, but the part about [Angular workspace configuration](https://angular.io/guide/workspace-config) is a bit lacking compared to the rest. For example: Explaining the pros and cons.

One such advantage is that when you split your project, it builds everything when you use `ng serve` but when you run `ng test` it will only run the tests inside the application and not the libraries.

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
