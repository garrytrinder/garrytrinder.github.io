---
layout:         post
title:          Keeping your fork up to date
category:       Development
tags:           [Git, Contributing]
permalink:      /:year/:month/:title
published:      true
---

When contributing to an open source project one of the regular tasks that you need to perform is ensuring that your fork is up to date to help avoid merge conflicts when merging your code contributions.

As a maintainer and contributor to the [Office 365 CLI](https://aka.ms/o365cli) project, this is a task which I perform weekly in-line with our release cadence, ensuring that I am creating any new branches from the latest version of the source code.

We currently release a new beta version every Sunday, updating our `dev` branch and a monthly release which updates our `master` branch. 

As an example, our last release contained 10 commits to the `dev` branch, meaning that my forked version of the `dev` branch was now 10 commits behind and missing those commits.

![](/public/img/git/office365-cli-commits.png){: .center-image }

## Add the upstream remote

When you first create a fork and clone this to your local machine, there is no link between your fork and the repository that it has been created from.

For us to be able to pull down updates from the original repository, we need to ensure that we have that link.

This link is established by creating a new remote called `upstream` targeting the original repository.

```
git remote add upstream https://github.com/pnp/office365-cli.git 
```

> To verify that the upstream link has been establised you can use `git remote -v` to return a list of the remotes created on your local repository

Now that this link is established, we can pull down the latest source from the original repository to our machine.

```
git fetch upstream
```

This will pull down all the branches from the upstream which we can use to rebase our local out of date branches with.

## Keep dev in sync

To update our local `dev` branch with the latest changes in the upstream, we can use the `git pull` command, using the `--rebase` switch and define the remote and branch that you want to use to rebase from.

Rebase re-plays the commits from the latest source code on top of your branch, adding the missing changes.

After rebasing, your local dev branch will be the same as the branch in the `upstream` repository matching the same number of commits on your local machine.

We can then push the local branch up to GitHub local using `git push`.

You will now see that your `dev` branch in your fork on GitHub.com now matches the number of commits.

```
git checkout dev
git pull --rebase upstream dev
git push
```

## Keep master in sync

You can easily repeat the same process for the `master` branch using the same approach.

```
git checkout master
git pull --rebase upstream master
git push
```

## Keep old branches in sync

If you have old branches, maybe a feature branch that you are still working on but want to keep up to date, you can use the same steps but target the upstream dev branch when rebasing instead.

```
git checkout feature-branch
git pull --rebase upstream dev
git push --force
```

The `--force` switch is required here if you have previously pushed your old branch to your fork on GitHub.com, this will replace the branch on GitHub with your updated local branch which contains the commits from the upstream dev branch, the updates, and your own commits made to your feature branch, your changes.

## Keep your upstream in sync

As time moves on, the upstream will be updated after a release and you need to keep this in sync on your local machine.

When that changes, you will need to ensure you fetch the latest changes onto your local machine before you then rebase any branches.

```
git fetch upstream
```