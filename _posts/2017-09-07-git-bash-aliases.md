---
title:  "AutoMapper Wiki"
header:
categories: 
  - Software-Development
tags:
  - git
  - bash
  - C#
---

![header](/assets/posts/2017-09-07-git-bash-aliases/header.jpg)

## Introduction

Do you have a have a distaste for typing the same things over and over again? I'm sure you do! Do you have a distaste for typing the same things over and over again? Who doesn't?! 

This article is the result of me typing git commands.. and well.. being lazy about it!

I'll show you how to configure bash with bash aliases so that you can quickly preform your git commands without the ho-hum of whole words!

## Prerequisites

* Windows 10
* https://git-scm.com/download/win

## Aliases

Lets take an simple command

```
git add .
```


Git allows for aliases but you have to type a little more  See [Git Basics - Git Aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) for more info on that.

```
git a
```

Instead using bash aliases you can type something like

```
ga
```

If you think this doesn't matter, this article is not for you! For the rest of us lazy-fingered devs, proceed to the steps below!

## Cmder

## VS Code Terminal

To be able to benefit from our git bash aliases in VS Code we must overwrite a couple user settings.

Open settings by using (Ctrl + ,) or 
1. File Menu
2. Preferences
3. Settings (Ctrl ,)

Then paste the following lines into the right settings override window.
```csharp
{

...

//Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
// start a login shell to pick up aliases from .bash_profile
"terminal.integrated.shellArgs.windows": ["--login"]
}
```

## References

https://jonsuh.com/blog/git-command-line-shortcuts/
https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases
