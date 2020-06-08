---
title: Create An Angular App With Sidebar, Header, and Footer with Angular Material
excerpt: ''
header:
  teaser: ''
categories: []
tags:
- Angular Material
- UI
- Angular
comments: false

---
### Intro

Starting a new Angular application with a blank canvas can be intimidating. In this tutorial, I will explain how to build the basic structure of your application and give a template for you to get started with for your own projects!

### Prerequisites

* Angular CLI
* Node JS
* NPM

### Create Application

1. Open a command prompt and navigate to the location you'd like to place your project. I place mine in a C:/Projects location.
2. `ng new [yourappname]`

### Add Shared Module Components

Make sure to follow the [https://angular.io/guide/styleguide](https://angular.io/guide/styleguide "https://angular.io/guide/styleguide") when adding components. Here we will add our "shared" components for the app.

This will help when important things like Angular Material into feature components so that you don't have to do that multiple times.

This module should contain things like:

* components
* directives
* pipes
* models

### Add Core Module

This will help keep your app module clean and give separation to tasks needed by the app.

This module should contain things like:

* authentication
* guards
* http
* interceptors
* services
* layout

    ng g module core --module app

Modify the CoreModule class export to ensure it is only important via the AppModule.

    import { NgModule, Optional, SkipSelf } from '@angular/core';
    import { CommonModule } from '@angular/common';
    
    @NgModule({
      declarations: [],
      imports: [
        CommonModule
      ]
    })
    export class CoreModule {
      constructor( @Optional() @SkipSelf() parentModule: CoreModule) {
        if (parentModule) {
          throw new Error('CoreModule has already been loaded. You should only import Core modules in the AppModule only.');
        }
      }
    }

### Add Angular Material

    ng add @angular/material

### Add Layout Core Components

    ng g component core/layout/header --export=true
    ng g component core/layout/nav-menu --export=true

[https://material.angular.io/components/sidenav/overview](https://material.angular.io/components/sidenav/overview "https://material.angular.io/components/sidenav/overview")

### Modify Components

header.component.html

    <mat-toolbar>
      <mat-toolbar-row class="toolbar">
        <div class="toolbar-section">
          Left Content
        </div>
        <div class="toolbar-section">
    	  Right Content
        </div>
      </mat-toolbar-row>
    </mat-toolbar>
    

header component styles

    .toolbar {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
    }
    
    .toolbar-section {
      display: flex;
      flex-direction: row;
    }
    

nav-menu.component.html

    <mat-nav-list>
      <mat-list-item>Realtime</mat-list-item>
    </mat-nav-list>
    

app.component.html

    <mat-sidenav-container class="container">
    
      <mat-sidenav mode="side" opened>
        <h2>App Name</h2>
        <app-nav-menu></app-nav-menu>
      </mat-sidenav>
    
      <mat-sidenav-content>
        <app-header></app-header>
        <router-outlet></router-outlet>
      </mat-sidenav-content>
    
    </mat-sidenav-container>
    

app component styles

    .container {
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      background: #eee;
    }

### References

[https://medium.com/@rajaramtt/angular-style-guide-best-practices-e7ec08ad3226](https://medium.com/@rajaramtt/angular-style-guide-best-practices-e7ec08ad3226 "https://medium.com/@rajaramtt/angular-style-guide-best-practices-e7ec08ad3226")

[https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/](https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/ "https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/")