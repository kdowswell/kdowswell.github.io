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
git commit --message
```

Git allows for aliases but you have to type a little more.

```
git cm
```

With bash, you can type something like

```
gcm
```

If you think this doesn't matter, this article is not for you! For the rest of us lazy-fingered devs, proceed to the steps below!

## Steps

Okay, assuming you've installed git for windows and have git bash installed. Lets knock out a quick config file that will get you on your way to typing less and coding more!

1. Open git bash
    * You can do this from you start menu by just searching for 'git bash'
2. Run these commands
    ```
    cd ~/
    notepad .bash_profile
    ```
4. Paste the following into the notepad file and save it
    ```bash
    # ----------------------
    # Git Aliases
    # ----------------------
    alias g='git'
    alias ga='git add'
    alias gaa='git add .'
    alias gaaa='git add --all'
    alias gau='git add --update'
    alias gb='git branch'
    alias gbd='git branch --delete '
    alias gc='git commit'
    alias gcm='git commit --message'
    alias gcf='git commit --fixup'
    alias gco='git checkout'
    alias gcob='git checkout -b'
    alias gcom='git checkout master'
    alias gcos='git checkout staging'
    alias gcod='git checkout develop'
    alias gd='git diff'
    alias gda='git diff HEAD'
    alias gi='git init'
    alias glg='git log --graph --oneline --decorate --all'
    alias gld='git log --pretty=format:"%h %ad %s" --date=short --all'
    alias gm='git merge --no-ff'
    alias gma='git merge --abort'
    alias gmc='git merge --continue'
    alias gp='git pull'
    alias gpr='git pull --rebase'
    alias gr='git rebase'
    alias gs='git status'
    alias gss='git status --short'
    alias gst='git stash'
    alias gsta='git stash apply'
    alias gstd='git stash drop'
    alias gstl='git stash list'
    alias gstp='git stash pop'
    alias gsts='git stash save'

    # ----------------------
    # Git Functions
    # ----------------------
    # Git log find by commit message
    function glf() { git log --all --grep="$1"; }
    ```

## Cmder

To use bash with cmder you can specify bash to be your startup terminal.

![startup settings](/assets/posts/2017-09-07-git-bash-aliases/cmder-startup.jpg)

In my bash settings I had to put the following below instead of the default to get bash to load. It seems like they have an outdated git-for-windows directory reference. I also had issues with the variables used so I just kept it simple with the following command to open bash. You can specify the start directory to whatever you'd like.

```
C:\Program Files\Git\git-bash.exe -new_console:d:C:\
```

![startup settings](/assets/posts/2017-09-07-git-bash-aliases/cmder-bash.jpg)

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

## Summary

So there you have it. git bash aliases to let you fly through your git commands. I'm going to be using this for a while but might explore using a solution like <https://gist.github.com/mwhite/6887990> instead to allow for using bash shorthand commands while having extended ability to use git aliases in other terminals.

```bash
if [ -f /etc/bash_completion ] && ! shopt -oq posix; then
    . /etc/bash_completion                                                                                                                                                                
fi


function_exists() {
    declare -f -F $1 > /dev/null
    return $?
}

for al in `__git_aliases`; do
    alias g$al="git $al"
    
    complete_func=_git_$(__git_aliased_command $al)
    function_exists $complete_fnc && __git_complete g$al $complete_func
done
```

## References

* <https://gist.github.com/mwhite/6887990>
* <https://jonsuh.com/blog/git-command-line-shortcuts/>
* <https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases>
* <http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/>
* <https://github.com/GitAlias/gitalias>
* <https://stackoverflow.com/questions/2114111/where-does-git-config-global-get-written-to>
