# Installing git on Windows

Installing git on Windows is a straight forward process, however there are a few things that you should change in the installation wizard. Download the 64-bit installer from git-scm.com and execute the installer, as you 

- Choosing default editor used by Git
  - If you are not familiar with Vim, choose your text editor of choice Visual Studio Code would be a great choice.
- Adjusting the name of of the initial branch in new repositories
  - Choose override the default branch name for new repositories and confirm main as the default name
- Choosing HTTPS transport backend
  - Choose Use the Native Windows Secure Channel library
- Configuring the line ending conversions
  - Choose Checkout as-is, commit this-style line endings

After finishing the installation, you will find some new git applications in your Start Menu, `git GUI` and `git Bash`. Open `git Bash` which will launch a command line prompt which you can execute `git` commands in to create repositories and make commits.