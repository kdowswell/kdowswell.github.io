---
title: Angular 9 Theme With CSS Variables
excerpt: ''
header:
  teaser: ''
categories:
- Software Development
tags:
- UI
- SCSS
- CSS
- Angular
comments: false

---
### Intro

Angular Material doesn't work with CSS Variables out of the box. So I will be describing how I use a library to add this ability to give more flexible theme options with CSS variables.

### Prerequisites

* An Angular App

### Add Angular Material Helper Library

[https://github.com/johannesjo/angular-material-css-vars](https://github.com/johannesjo/angular-material-css-vars "https://github.com/johannesjo/angular-material-css-vars")

Follow the steps on this github readme.

I have mine working with the root app component having `class="isDarkTheme"` on a container div around everything else.

### Create your color palette

[http://mcg.mbitson.com/](http://mcg.mbitson.com/ "http://mcg.mbitson.com/")

Use this color palette in your styles.scss file.

### Modify the styles.scss file

Add the palettes from the color generator 

Example:

    $mat-primary: (
        50 : #fff7e0,
        100 : #ffeab3,
        200 : #ffdd80,
        300 : #ffcf4d,
        400 : #ffc426,
        500 : #ffba00,
        600 : #ffb300,
        700 : #ffab00,
        800 : #ffa300,
        900 : #ff9400,
        A100 : #ffffff,
        A200 : #fff9f2,
        A400 : #ffe1bf,
        A700 : #ffd5a6,
        contrast: (
            50 : #000000,
            100 : #000000,
            200 : #000000,
            300 : #000000,
            400 : #000000,
            500 : #000000,
            600 : #000000,
            700 : #000000,
            800 : #000000,
            900 : #000000,
            A100 : #000000,
            A200 : #000000,
            A400 : #000000,
            A700 : #000000,
        )
    );

Add the angular material css vars lines below:

    @import '~angular-material-css-vars/public-util';
    @import '~angular-material-css-vars/main';
    
    @include init-material-css-vars();
    
    @include mat-css-set-palette-defaults($mat-primary, 'primary');
    @include mat-css-set-palette-defaults($mat-accent, 'accent');
    @include mat-css-set-palette-defaults($mat-red, 'warn');