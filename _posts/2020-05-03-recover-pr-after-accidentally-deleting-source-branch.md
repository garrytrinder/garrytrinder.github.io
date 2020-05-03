---
layout:         post
title:          Recovering a pull request after accidentally deleting the source branch
category:       Git
tags:           [Git]
permalink:      /:year/:month/:title
published:      true
---

If you are a regular contributor to an open source project on GitHub pushing code changes via pull requests, it is a good idea to delete the branches that have been merged and no longer needed.

I like to make sure that I keep my repositories up to date and employ good branch hygiene, making sure that I only have branches that I am working on in my GitHub forks and locally on my machine. 

Currently we release a new version of the Office 365 CLI on a weekend, so I've got into a habit of using this day to sync my fork, ensuring that both the `master` and `dev` branches are up to date and cleanup up any branches that I don't need anymore.

Now reading the title of this post, I'm sure you can now imagine what prompted me to write it... yes, you guessed it, I deleted a branch that I still needed, both from my fork in GitHub and locally. To make matters worse, deleting this branch automatically caused my open pull request causing it to be instantly closed.


![](/public/img/git/deleted-source-branch.png){: .center-image }


As it turns out, this was fairly simple to fix. Every commit that you make in Git is uniquely recorded with a SHA-1 checksum and we can use this to create a new branch from, essentially recreating the branch from a point in time.

> **git checkout -b &lt;branch&gt; &lt;start_point&gt;**
>
> Create a new branch named &lt;branch&gt; and start it at &lt;start_point&gt;

The important part is obtaining the commit SHA-1 checksum of my commit. I was able to get this from my closed pull request by viewing the `Commits` tab on the pull request and copying the commit SHA-1 using the `copy` button. 


![](/public/img/git/copy-commit-sha1.png){: .center-image }


Using the `git checkout` command, I was able to then re-create the branch locally and push the branch back up to my fork in GitHub, which restored the branch that my pull request was referencing. 


```
git checkout -b auth-filestorage a1a12389bbefdf1aa197d04940b48d8641bbeae7
git push --set-upstream origin auth-filestorage
```


![](/public/img/git/restored-branch.png){: .center-image }


This then allowed my to reopen my pull request 🙌🏻


![](/public/img/git/reopen-pull-request.png){: .center-image }


Crisis averted.
