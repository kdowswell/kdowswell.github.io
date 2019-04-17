---
title: Jekyll on GitHub Pages
excerpt: Publish new content to your blog hosted on GitHub Pages for FREE!
header:
  teaser: /assets/posts/2017-08-08-jekyll-on-github-pages/header.jpg
categories:
  - Software-Development
tags:
  - Jekyll
comments: true
published: true
---

![header](/assets/posts/2017-08-08-jekyll-on-github-pages/header.jpg)

## Introduction

I've always been looking for easy ways to start blogging. Wordpress is nice, but it requires hosting costs and admin dashboards to manage your site that just seem like too much effort. Sites like Medium are great, but you don't own the content and are at the mercy of their servers to host your content for its lifetime.

So this brings us to a third option, hosting your blog on GitHub Pages using Jekyll on Windows. This strategy requires an understanding of the command line but that's it. After you've followed the steps below, you'll be able to simply publish new content to your blog hosted on GitHub Pages for FREE!

Test123

## Installation

1. Open PowerShell as Administrator and run
    ```
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    ```
2. Open Command Prompt and run the following and follow prompts to install Ubuntu
    ```
    bash
    ```
3. Run the following in bash
    ```
    sudo apt-get update -y && sudo apt-get upgrade -y
    sudo apt-add-repository ppa:brightbox/ruby-ng
    sudo apt-get update
    sudo apt-get install ruby2.3 ruby2.3-dev build-essential
    sudo gem update
    sudo gem install jekyll bundler
    ```

## Create Your Site

You should now have jekyll installed. You can check this by running
```
jekyll -v
```

In bash change directory to a location you'd like to make your site then run. It will create a folder named whatever you call your site.
```
jekyll new my_blog
```
cd to that directory and run via bash
```
bundle install
```

## Host on GitHub

Create a new repository your_username.github.io

Run the following in your site directory
```
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/your_username/your_username.github.io.git
git push -u origin master
```

## Resources

* <https://jekyllrb.com/>
* <https://pages.github.com/>
* <https://jekyllrb.com/docs/windows/>
* <https://kramdown.gettalong.org/syntax.html>
* <https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf>
