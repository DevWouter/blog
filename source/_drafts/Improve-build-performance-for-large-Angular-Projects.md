---
title: Improve build performance for large Angular projects
tags:
    - Angular
    - Programming
    - Performance
# TODO 
# [ ] Add intro about why we need to do this
# [ ] Test it in a large scale project.
---

<!-- Tell why we need-->

```sh
ng new ang-workspace --createApplication="false"
cd ang-workspace
ng generate application ang-app 
ng generate library ang-lib
```

When the above is done we have a project with 1 application and 1 library.

We then modify `app.component.html` so that we have library component. Simply replace it all.

```html ang-workspace\projects\ang-app\src\app\app.component.hml
<h1>Hello world</h1>
<lib-ang-lib></lib-ang-lib>
```

And of course we need to include the library module in the application module.

{% codeblock ang-workspace\projects\ang-app\src\app\app.module.ts lang:cs mark:13 %}
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

When you now run `ng serve` it will automatically build the library and serves the website.
However if you run `ng test` it will only run the tests inside the `ang-app`.
So to test your library you will need to run `ng test ang-lib`.

Personally I don't like having an extra window for unit tests, so I prefer to run
```bash
$ ng test ang-lib --browsers ChromeHeadless
```