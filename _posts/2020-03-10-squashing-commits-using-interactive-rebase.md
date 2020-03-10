---
layout:         post
title:          Squash your commits using git interactive rebase
category:       Development
tags:           [Git, Contributing]
permalink:      /:year/:month/:title
published:      true
---

This post will show you how to merge all of your commits into one to help make your pull requests lighter and help keep the history clear for others to track changes. 

Every commit you make, saves any changes to a local git repository, helping build up a history log of what has happened over time.

It is good practice to commit changes frequently as we work in our feature branches so that we can keep track of the changes we have made and make it easier to roll back to a working state. That said, commiting frequently does have its drawbacks, it can lead to pull requests being created with several or if it is a larger change, potentially hundreds of commits. 

This level of detail may make great sense to someone who has written the code, however this maybe confusing the someone who is required to review those changes as part of a pull request code review. 

Does the reviewer really need to know that you made 5 commits to get something working or another 3 commits to fix typos? Probably not.

Therefore it is good practice that before submitting a pull request, you tidy the history of your feature branch to just represent all the changes you have made in a single commit. You will find that some open source projects will encourage this, such as the [Office 365 CLI](https://github.com/pnp/office365-cli) who operate a `One PR = One Commit` rule for pull requests helping keep the commit history nice and clean for all to see.

![](/public/img/git/office365-cli-commits.png){: .center-image }

So how can this be done?

By using something called, **git interactive rebase**, which we can use to help re-write the commit history in our local repository.

Consider this scenario, I am writing a blog post in a new feature branch, I create the basic page for the post with a title and commmit this change. I then start to write my blog post, after a while I take a break, so I commit the changes made, when I return I complete the rest of the post and commit those changes again. After another break, I return to read through my post and spot some typos, so I make those changes and again commit them.

This is a fairly common scenario, but as you can see I have so far created 4 commits and viewing the history, `git log --oneline`, you would see something like this...

```
37b5bf3 (HEAD -> your-branch) Fixed typos
fdabd0d Complete
67a35d7 Stopped for break
83bddef Initial commit
```

So based on the above git log output, we can use the `rebase` command and its interactive mode to re-write our history.

Executing `git rebase -i HEAD~4`, where `4` represents the number of commits you want to go back in your history to re-write. The rebase process will be started and you will be entered into an interactive editor, which will look something like this...

```
pick 83bddef Initial commit
pick 67a35d7 Stopped for break
pick fdabd0d Complete
pick 37b5bf3 Fixed typos

# Rebase 83bddef..37b5bf3 onto 37b5bf3 (4 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

> The key point to note here is that the editor displays the commits in reverse order starting from 4 commits back, which was defined by `HEAD~4`, they also contain a commit command all set to `pick` which is the default.

What we want to do is keep a single commit but merge all other commits into one, to do this we will edit the commands next to each commit, except the top one, in the editor.

Using your keyboard, press `s` to go into `INSERT` mode, replace `pick` on all commit lines except the top one with `fixup` or `f` and replace the top commit with `reword` or `r`, then press `esc` to leave `INSERT` mode. You will end up with something like this...

```
reword 83bddef Initial commit
fixup 67a35d7 Stopped for break
fixup fdabd0d Complete
fixup 37b5bf3 Fixed typos
```

So what is going on here? 

The above commands squash the three commits into the top commit discarding any commit messages from the log (`fixup`) and also give us the chance to amend the commit message of the remaining commit to something more appropriate (`reword`).

Press `:` followed by `x` and press `enter`, this will save your changes and start the rebase. 

Next, you will be presented with a screen displaying the commit message of the commit you marked with `reword`. Edit the commit message in the same way as you did for the previous step and save your changes in the same way.

You should now recieve a success message in the console, `Successfully rebased and updated refs/heads/your-branch.`. 

If you view the git log again, `git log --oneline`, you will now find just a single commit, with the other commits no longer showing as they are now merged with the one remaining commit.