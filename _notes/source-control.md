# Version Control System

A common feature of software that we use today and one of the most important features we look out for is the undo button to revert the last change we made, with some software being able to undo multiple changes to recover changes over a longer period of time.

We can undo mistakes that happened minutes ago, but what happens if we want to undo changes that happened over a longer period of time, what if we want to understand why changes were made, who made the changes or even roll back to a previous state?

This is where version control systems come in, they allow us to create repositories to store our files, track changes made over time and provide us with assurances that we can restore or view a version of a file at a given point in time, understand changes made to those files over time and who made them.

[git](https://git-scm.com) is the most popular and widely used version control system, it is a command line interface, that is open source and works on any operating system.

Changes made to files within a Git repository are grouped together in commits, a single commit can include changes made to multiple files, each commit representing a point in time like a photo, creating a timeline of changes over time all tracked in a commit log. It is this log that enables us to view the differences between files and provide a way of reverting back to a previous state should a mistake be made.

It's popularity has seen the rise of the [GitHub](https://github.com) repository service as the place to share and collaborate, which is underpinned by the Git version control system which it takes its name from. So popular that Microsoft purchased GitHub for $7.5bn in 2018. Git is also used as the primary version control system used in Azure DevOps, another code repository service owned by Microsoft. Version control and repository sharing is big business.

Primarily `git` is seen as a developer tool and in the main, it is, however this is not to be seen as the case, the vast majority of employees are now knowledge workers, we create, save, edit, save again on a daily basis, having a version control system to visually highlight and track changes can become invaluable whether that is working on code files, documents, images and another other assets.

## Getting Started

The first place to start is to install Git onto your machine, download the installer from the [Git](https://git-scm.com) website and follow the install wizard.

To confirm that `git` has been installed on your machine, open up `git bash`, which is installed by the installer and execute `git --version`, if all is well you will see the version returned at the prompt.

If you want to see the git help files, you can use `git --help` to view this in the prompt, alternatively you can access the same help content in the git [reference](https://git-scm.com/docs) on the web.

## Create your repo folder

Now that you have git installed you can run git commands against any folder on your file system, however the first step is generally to create a folder to store the repositories that you create as it is generally seen as best practice to group your repositories under a single folder, I like to create a folder called `repos` which I can then create folders in that I then convert into repositories.

In `git bash`, create a new folder called `repos` by executing `mkdir repos` and then changing to that directory using `cd repos`.

## Create your first repository

NOw that we are inside the `repos` folder, we can create a new folder that we will convert into a repository.

Create a new folder called `my-first-repo`, by executing `mkdir my-first-repo` and changing into that directory by executing `cd my-first-repo`.

As we are inside the `my-first-repo` folder, we can convert it into a repository by executing `git init`, you will receive confirmation that an empty Git repository has been initialized in the current directory. 

Executing `git init` creates a special hidden folder in the `my-first-repo` folder called `.git`, it is here where all of the commit activity in the repository is tracked as well as information about repository branches, of which a default branch `main` was also created when you executed the `git init` command, this is shown after the folder path as `(main)`.

You cannot have a git repository without a `default` branch.

## Your first commit

As we have an empty repository, lets create a file in the folder and see what happens.

I not going to assume that you have a fancy text editor installed, so lets open notepad and create a markdown file. Markdown is a plain text markup language used for creating content on the web which is very simple and easy to pickup, very popular with bloggers.

To create the file and open notepad, execute `notepad hello-world.md`, selecting `yes` to the prompt to save the file and add the following contents to the file, saving the file again.

```md
# Hello World

This is my **first** _markdown_ file!

## What have I learned so far

 - How to install git
 - How to open [git](https://git-scm.com) bash
 - How to create folders and change directory
 - How to initialize an empty git repository
 - How to create a basic markdown file!
 - Basic markdown syntax
```

Close notepad and go back to `Git Bash` and execute `git status`