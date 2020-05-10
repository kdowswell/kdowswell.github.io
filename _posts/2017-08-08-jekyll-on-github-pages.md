---
title: Jekyll on GitHub Pages
excerpt: Publish new content to your blog hosted on GitHub Pages for FREE!
header:
  teaser: "/assets/posts/2017-08-08-jekyll-on-github-pages/header.jpg"
categories:
- Software-Development
tags:
- Jekyll
comments: true

---
![header](/assets/posts/2017-08-08-jekyll-on-github-pages/header.jpg)

_Updated: 5/10/20 Added new Ruby Installer for simple setup and section about Writing Posts._

## Introduction

I've always been looking for easy ways to start blogging. Wordpress is nice, but it requires hosting costs and admin dashboards to manage your site that just seem like too much effort. Sites like Medium are great, but you don't own the content and are at the mercy of their servers to host your content for its lifetime.

So this brings us to a third option, hosting your blog on GitHub Pages using Jekyll on Windows. This strategy requires an understanding of the command line but that's it. After you've followed the steps below, you'll be able to simply publish new content to your blog hosted on GitHub Pages for FREE!

## Installation

1. Download Ruby Installer

   [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/ "https://rubyinstaller.org/downloads/")
2. Run the installer
   * Keep all options checked during installation
3. After installer runs a cmd window will open up, hit `Enter`
4. After those installations finish, open a new cmd window
5. run `gem install jekyll bundler` in the cmd window

## Create Your Site

You should now have jekyll installed. You can check this by running

    jekyll -v

In bash change directory to a location you'd like to make your site then run. It will create a folder named whatever you call your site.

    jekyll new my_blog

cd to that directory and run via bash

    bundle install

## Host on GitHub

Create a new repository your_username.github.io

Run the following in your site directory

    git init
    git add .
    git commit -m "first commit"
    git remote add origin https://github.com/your_username/your_username.github.io.git
    git push -u origin master

## Writing Posts

I have tried using VS Code, Prose, and most recently Forestry for creating content. I really like [https://app.forestry.io/](https://app.forestry.io/ "https://app.forestry.io/"). It gives a very easy to use text editor and allows you to switch between markdown and wisiwig editors. It has great resource management and makes saving posts and updating content super easy. 

I also pair Forestry up with the Chrome extension [Grammarly](https://www.grammarly.com/). This gives great spelling and sentence structure feedback as you are creating posts!

## Resources

* [https://jekyllrb.com/](https://jekyllrb.com/)
* [https://pages.github.com/](https://pages.github.com/)
* [https://jekyllrb.com/docs/windows/](https://jekyllrb.com/docs/windows/)
* [https://kramdown.gettalong.org/syntax.html](https://kramdown.gettalong.org/syntax.html)
* [https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)