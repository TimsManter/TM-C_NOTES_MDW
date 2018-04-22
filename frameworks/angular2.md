# Angular2

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-02
* @BasedOn: [Angular Quickstart][basedon]

[basedon]: https://angular.io/docs/ts/latest/quickstart.html

<!-- TOC -->

1. [Overview](#overview)
2. [Component](#component)

<!-- /TOC -->

## Component

`app.component.ts`:
```ts
import { Component } from  '@angular/core';

@Component({
    selector: 'my-app',
    template: `<h1>Hello {{name}}</h1>`
})

export class AppComponent { name = 'Angular'; }
```

`app.module.ts`:
```ts
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';

@NgModule({
    imports:      [ BrowserModule ],
    declarations: [ AppComponent ],
    bootstrap:    [ AppComponent ]
})

export class AppModule { }
```

`main.ts`:
```ts
import { plarformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { Appmodule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule);
```