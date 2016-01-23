---
layout: post
title: Safety Net with Git Stash
permalink: git-stash-safety-net
---

Git is great. If you're not using it yet, you should start now. Even if you're not working with other developers git is awesome for showing your progress and helping you revert back to a previous point if that need should ever arise. 

One technique that I started using was using `git stash` to give myself a safety net if I was going to make some big changes. This is especially useful if you are working on a large code base.

### How to do it

Let's say you're working on a large existing project that is new to you. In the process of trying to fix a bug you have made quite a few changes and things are looking better but they are not quite there yet. You are not ready to make a commit but you also don't want to make things worse than they are right now. You need a save button. Use git stash. 

```
$ git stash save [message]
$ git stash apply

```

What we did here was first stashed all of our working changes (with an optional message to remind us of what we were doing), and then immediately un-stashed our changes.  But by using `git stash apply` instead of `git stash pop`, we haven't deleted the stash. We essentially have a 'save point' of where we are at right now.

Now let's say you move forward and make more changes, but you realize the changes you made after the 'save point' have been a regression and you want to reset. Easy:

```
$ git checkout -- .
$ git stash apply
```

The `git checkout -- .` command discards all your working changes, and then the `stash apply` brings back your work up to your 'save point'. Now things are back to where you liked them and you can start trying new changes to finally squash that bug.

Just a word of caution.  If you haven't saved your work with a `stash` or `commit` or otherwise, doing `$ git checkout -- .` will cause you to lose all of your progress. Don't say I didn't warn you.