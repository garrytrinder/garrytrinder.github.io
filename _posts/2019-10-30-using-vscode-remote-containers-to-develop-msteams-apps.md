---
layout:         post
title:          How to use Visual Studio Code Remote Containers to develop Microsoft Teams apps
category:       Development
tags:           [Microsoft Teams,Visual Studio Code,Remote Containers,Docker]
permalink:      /:year/:month/:title
published:      true
---

This post will guide you through the process of creating and configuring a remote development container within Visual Studio Code for Microsoft Teams app development. The 'Visual Studio Code Remote - Containers' extension lets you use a Docker container as a full-featured development environment. 

### Prerequisites

This guide assumes that you have Docker already installed configured to use Linux containers and is running, see [Docker Install](https://docs.docker.com/v17.12/install/) for more detail.

### Create the project folder

First we need to create an empty folder for our project.

- Open a terminal session
- Create a new folder for your project
  - `mkdir teams-remote-container` 
- Change into project directory
  - `cd teams-remote-container` 
- Open folder in Visual Studio Code
  - `open .`

### Install VSCode Remote Development Extension Pack

To enable the remote development functionality within Visual Studio Code you will need to install an extension from Microsoft, see [Remote Development Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) on the marketplace.

- Open Extensions marketplace from the Side Bar
- Search for `Remote Development`
- Install the extension

### Add Development Container Configuration Files

Next step is to create a base remote container configuration within the empty project.

- Open the command palette
- Search for and select the `Remote-Containers: Add Development Container Configuration Files...` command
- From the `Add Development Container Configuration Files` menu, type `node` and select `Node.js (latest LTS) & Typescript`

![](/public/img/teams/create-base-container.gif){: .center-image }

After completing the above steps you will find a new folder in your project folder called `.devcontainer` which contains two files, `devcontainer.json` and `Dockerfile`.

> A prompt will be displayed asking if you want to reopen the project in a container, ignore this

### Update the Dockerfile

Next step is to update the base Dockerfile to use a lighter base Docker image Node.js and include the dependencies required for Microsoft Teams app development.

- Open `Dockerfile`
- On line 6, replace `FROM node:lts` with `FROM node:slim`
- On line 37, replace `&& npm install -g tslint typescript \` with `&& npm install -g tslint typescript yo gulp-cli generator-teams \`
- Save the file

### Update devcontainer.json

Next step is to change the VSCode configuration file which VSCode will use when instrucing Docker to build and start the container.

- Open `devcontainer.json`
- Update `name` to from `Node.js (latest LTS) & TypeScript` to `Microsoft Teams Development`
- Uncomment line 14 and replace `"appPort": []` with `"appPort": [3007,9229],`
- Uncomment line 17
- Uncomment line 22 and replace `"runArgs": [ "-u", "node" ],` with `runArgs": [ "-u", "node" ],`
- Save the file

### Reopen the project

Now that we have configured our remote container, we are now ready to reopen the project inside the Container.

- Open the command pallete or click the Remote Container icon (`><`) in the bttom left of the status bar
- Search for and select `Remote-Containers: Reopen in Container`

VSCode will instruct Docker to build the Dockerfile, generating an image with all the required dependencies installed, reopen the project within the context of the container and open an interactive bash terminal session.

![](/public/img/teams/reopen-project.gif){: .center-image }

### Scaffold your Microsoft Teams project

Now that the container is running, we can run commands inside it to scaffold our new project. 

You do this by executing `yo teams` from the terminal session to start the Microsoft Teams Yeoman generator.

![](/public/img/teams/scaffold-project.gif){: .center-image }

After your project has been created, run `npm run-script debug` to start the ngrok server. Opening a browser window and navigating to `http://localhost:3007` will display the debug web server running within the container.

![](/public/img/teams/localhost-ngrok.gif){: .center-image }

### Update devcontainer.json to apply project environment variables in container

When a new project has been created a `.env` file is created, as we are running in a container we need to tell Docker to use this file to update the environment variables within the running container. 

> This step is important for when you want to package your app as environment variables are used in the packaging process

- Open `devcontainer.json`
- On line 22, replace `runArgs": [ "-u", "node" ]` with `runArgs": [ "-u", "node", "--env-file=.env"]`
- Save file
- Open the command pallete, search for and select `Remote-Containers: Rebuild Container`

### Closing connection

When you are done, you can close the project and the container by clicking on the DevContainer icon in the bottom left of the status bar and selecting `Close remote connection`
