+++
date = "2015-08-27T11:52:29+01:00"
draft = false
title = "git 4 Astronomers"

+++

## Why use version control

At the recent STFC summer school in Cardiff, I organized a python workshop. I encouraged all the attendees to use have a sensible way of keeping different versions of your code. Having used other methods, I particularly like Git. Having a backup of your code somewhere not on your computer is also a great idea. I highly recommend keeping your work in [GitHub](https://github.com). Instead of periodically copying your code somewhere manually, its a good be able to see all your revisions if you are away from your computer, or if (and it will happen) your computer dies at a critical moment.

## How to get Git

[GitHub have an easy guide on installing git](https://help.github.com/articles/set-up-git/). It also covers setting up a GitHub account. Its probably a good time to do that.

## How to use Git

If you have a folder with files in that you want to use version control with, its easy to start.
```bash
cd myfolder
git init
```
Easy. You now have a new *repository* which you can start adding things to.

Lets have a look at what git thinks about our folder:
```bash
git status
```
If you had files in that folder, you'll see a list of `untracked` files.

# Add version tracking to files
You have to tell git which files you want to keep track of. You can do this in a number of different ways:

Add an individual file
```bash
git add myfile.py
```

Add all files in the current directory
```bash
git add .
```

Add all files in all subfolders of your project.
```bash
git add -A
```

## Making revisions
So, you've added all those files. Now you start editing your code. When you have done some editing, writing, deleting and your code is working (you probably don't want to deliberately save a revision which is broken - you'll do that unconsciously quite often anyway!). Save your files normally.

Now comes the git part:

You'll add all your edited files and add a helpful message:
```bash
git commit -am "Fixed a bug in somefunction and added falangy feature"
```
You now have a nice revision and at any point in the future, you can look at the code at this time.

This is actually a short hand (i.e. the `-am` flag) for adding *and* committing a revision. It only works for files you've previously added and only ones in the current directory. If you added some files in a different directory of the same project, you can use do:
```bash
git add -A
git commit -m "Fixed a bug in somefunction and added falangy feature"
```

## Revert to previous version
You've gone to all this effort to make your code to log all these different revisions, how do you revert to a previous edit. You might realise that your code is borked but it worked yesterday, or you might just want to look at the code you just committed before you changed it. As you would hope, its very easy.
```bash
git revert HEAD
```
This will undo the last commit you made. If you want to see all of the revisions you've committed and pick the one you need to revert first do:
```bash
git log
```
you will get a list of your different commits with long alphanumeric sequences next to them, and the message you added when you made the commit. Pick the one you want, copy the alphanumeric code and do the following:
```bash
git revert <alphanumeric code>
```
This will roll back the code to that point.

## Putting it in the cloud
If you want to share your project with people, or just have a cloud backup, I recommend using GitHub. GitHub have made a very good [step-by-step guide to making a repository on GitHub](https://help.github.com/articles/creating-a-new-repository/). Your repository will be made public by default. Normally you have to pay for private repositories, but if you are at a University you can get a load of [free, private repositories from GitHub](https://education.github.com/). Which is nice.

When you have set up your repository on GitHub you need to tell the version on your computer that you'll be using github to store it in the cloud.

```bash
git remote add origin <name of your repository>
```
The URL to your repository will look like `git@github.com:username/repositoryname.git`.

Now you want to copy all of the revisions you've been saving to GitHub. This is called *pushing* your code.
```bash
git push origin master
```

From that moment on everytime you have your code in a good place (i.e. not knowingly buggy), this is your workflow:
```bash
git add -A
git commit -m "My latest changes"
git push
```
That saves revisions and then copies them to GitHub.

### GitHub App
Although I've talked entirely about working on the command line here, I mostly use a free application, [GitHub Desktop](https://desktop.github.com/), developed by GitHub. It only works with GitHub repositories, but it is really nice.

### The End?
Thats a really, really quick getting started guide. I didn't mention:

* `git stash` - for temporarily storing edits while you `git pull` some changes
* `git branch` - particularly useful if you want to try something out with your code, but want to be able to get back to the working version quickly (e.g. you want to run it in its previous working state)
* `git merge` - Blend 2 branches together (e.g. you've just created and tested a new feature on a separate branch, and you're ready to incorporate it to the main code)
