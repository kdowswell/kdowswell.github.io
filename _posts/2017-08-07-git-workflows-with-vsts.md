---
title:  "Git Workflows With VSTS"
excerpt: "The gitflow branching and merging strategy has been great for us so far."
header:
  teaser: "/assets/posts/2017-08-07-git-workflows-with-vsts/header.jpg"
categories: 
  - Software-Development
tags:
  - git
  - VSTS
---

![header](/assets/posts/2017-08-07-git-workflows-with-vsts/header.jpg)

Recently my team at work migrated to git from TFS for our [VSTS](https://www.visualstudio.com/team-services/) repositories. The main reason we did this switch was to have an artifact to prove (in a [CMMI](https://en.wikipedia.org/wiki/Capability_Maturity_Model_Integration) inspection) that we did code reviews during our development process. We also wanted to adopt the [gitflow](http://nvie.com/posts/a-successful-git-branching-model/) workflow while working on our Scrum Sprints. The gitflow branching and merging strategy has been great for us so far. Below is a wiki for all of the scenarios we have during our Sprint. Enjoy!

## Git Scenario Workflows

### New sprint branch VSTS Method
New sprint has started and you need to see remote branches on your pc that have been added to the VSTS git repo
1. Create feature branch in VSTS from dev
naming conventions:
    * bugs/######-short-title-of-work-item
    * changes/######-short-title-of-work-item
    * features/######-short-title-of-work-item
    * spikes/######-short-title-of-work-item

    _Associate work item(s) to feature branch when creating branch._

2. Run git commands to see new branch and switch to it
    ```
    git checkout dev 
    git pull
    git checkout my-feature-branch-name
    ```

### New sprint branch Command-Line Method
New sprint has started and you want to start working on a feature branch without creating a branch on VSTS first.

1. Create feature branch in command line using the following command:
    ```
    git checkout -b "BranchName"
    ```

    **Naming Conventions for Branches**
    * bugs/######-short-title-of-work-item
    * changes/######-short-title-of-work-item
    * features/######-short-title-of-work-item
    * spikes/######-short-title-of-work-item

2. When you are ready to send your branch the server (after committing) run:
    
    ```
    git push
    ```
    *You will be given a command to enter to set the "upstream" of the server. Simply copy and paste the command into Cmdr and it will properly set it. Then run: git push*
         

3. Create a pull request for your newly pushed code
    Ensure to associate your Pull request to the work item for your branch. 
  
    _The difference with command line vs VSTS branch creation is that you associate your PBI's to your branch at the end (during PR creation) versus on creating of the branch in VSTS._
     

### Stage & Commit code changes to feature branch
When you have made changes and need to commit them to your local feature branch repo.
```
git status
     *if you want to see what changes you have currently made
git add .
     *to add all files currently modified in repo
git commit -m "comment for work I just completed"
```
Push code changes to feature branch
```
git pull
git push

```
### Get code from dev -> feature-branch
```
git checkout dev 
git pull 
git checkout feature-branch-name
git merge dev 
   solve merge issues, if any 
git push origin feature-branch-name
```

### Checkout remote feature-branch for pull request review etc
```
git checkout dev 
git pull 
git branch -r
    shows you the remote branches you can checkout
git checkout name_of_the_branch
    do not include origin prefix
```

If you would like to make changes set the branch upstream to the origin branch. Then you will be able to `git push` to that origin branch if needed.
```
git branch -u origin/name_of_the_branch
```

### Pull Request feature-branch -> dev
Use VSTS pull request feature in the branches area to submit a request. We use Branch Policies to ensure 1 person reviews it, a work item is linked, and the Merge Strategy is "No-fast-forward merge".

### Pull Request dev -> master
We use the "Swash Merge" VSTS Branch Policy under "Enforce a merge Strategy". This will condense all the changes in a pull request into one commit with one parent.

### Clear previous branches from PC
New sprint has started and you need to remove feature/bug/change branches that were added to your pc during the previous sprint.

#### Remove remote branches
```
git branch -r     
     *to see remote branches on your local pc
git remote prune origin
git branch -r
    *to verify changes were made
```

Or you can set a global git config setting which will prune your branches on fetch.

```
git config --global fetch.prune true
```

Then, every time you do a `git pull` or `git fetch` your origin branches will be pruned.

#### Remove local branches
```
git branch
    *to see local branches on your pc
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
git branch
    *to verify local branches were removed
```

## Resources

* <http://rogerdudler.github.io/git-guide/>
* <https://www.visualstudio.com/en-us/docs/git/gitquickstart-vs2017>
* <http://cmder.net/>
* <https://www.atlassian.com/git/tutorials/setting-up-a-repository>
* <https://www.atlassian.com/git/tutorials/merging-vs-rebasing>
* <https://try.github.io/levels/1/challenges/1>
* <http://git-school.github.io/visualizing-git/>