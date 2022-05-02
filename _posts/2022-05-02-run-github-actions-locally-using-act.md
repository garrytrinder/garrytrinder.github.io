---
layout:         post
title:          Run Github Actions locally using act
category:       Development
tags:           [git,github,actions,cli,microsoft,365]
permalink:      /:year/:month/:title
published:      true
---

I recently worked on refactoring the [CLI for Microsoft 365 Login](https://github.com/marketplace/actions/cli-for-microsoft-365-login) GitHub Action and one of the issues I came across during the development was being able to get fast feedback on the changes I had made. 

The only way I could test the changes was to commit my changes, push them to GitHub and manually trigger the workflow. 

Thankfully, [`nektos\act`](https://github.com/nektos/act/), is a command line tool that helps emulate the GitHub Actions environment locally using Docker,enabling you to trigger workflows without having to push to GitHub first.

As `act` relies on Docker, you will need this installed before installing it. You can install `act` using package managers such as `homebrew` or `chocolatey`, or via an installer which you can find on the latest [release](https://github.com/nektos/act/releases/tag/v0.2.26)page.

Once installed, you can trigger a workflow by executing `act` at the command line.

To test the Login action locally, I created the following `test.yml` file in the `.github/workflows` directory.

<script src="https://gist.github.com/garrytrinder/4512b846e198d8ffaa7547e26f371906.js"></script>

The workflow uses the `workflow_dispatch` event which is a manual trigger, it defines a single job that runs on the latest version of Ubuntu and has two steps, the first to checkout the local repository making the files available to the workflow runner and the second which executes the local version of our action denoted by `uses: ./`. The login step uses two GitHub Secrets which as passed as values into the `ADMIN_USERNAME` AND `ADMIN_PASSWORD` options.

To execute this workflow locally, we run...

`act workflow_dispatch -s ADMIN_USERNAME=username -s ADMIN_PASSWORD=password`
 
Where `workflow_dispatch` is passed as the tigger type (default is `push`) and pass two values as GitHub Secrets using the `-s` option.

![Terminal session showing the results of executing the above ](/public/img/cli-microsoft365/act-cli-action.png){: .center-image }

As we can see, we can now easily run our actions locally using `act`, and we can benefit from a much faster feedback loop 🚀