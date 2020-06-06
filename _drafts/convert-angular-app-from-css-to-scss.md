---
title: Convert Angular app from CSS to SCSS
excerpt: Started an app with CSS and want to change it to SCSS? Here is how to do
  it!
header:
  teaser: ''
categories:
- Software Development
tags:
- SCSS
- CSS
- Angular
comments: false

---

### Steps

1. Open your project in VS Code
2. Open cmd window for your src directory
3. Run `forfiles /S /M *.css /C "cmd /c rename @file @fname.scss"`
4. cd to your project directory root
5. Run `ng config schematics.@schematics/angular:component.styleext scss`
6. 