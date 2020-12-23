# Run CLI for Microsoft 365 in Docker

We are delighted to announce that all v3 and v3 beta images are available to download and use from the Docker Hub.

If this doesn't mean a lot to you right now, then let me explain why we feel this is a big deal.

Docker enables us to bundle a pre-configured version of CLI for Microsoft 365 together with all its dependencies into a single downloadable image, which you can be used to create and run an isolated environment on your machine, so you can use CLI for Microsoft 365 without cluttering your machine with dependencies.

Sounds great right?

To get started, you will need to have Docker installed and running on your host machine, do do that, checkout the guides over in the Docker [documentation](https://docs.docker.com/get-docker/), its free and can be installed on any operating system.

Once you have Docker running, open up your command prompt of choice and run the below command.

```
docker run --rm -it m365pnp/cli-microsoft365:latest
```

This command will instruct the Docker engine running on your host machine to attempt to start a container using an image called `m365pnp/cli-microsoft365`, as the `:latest` tag is specified we are also telling the engine to get the latest stable version of CLI image.

As the image won't exist on your host machine yet, Docker will automatically download the image from the Docker Hub where our images are publicly available, then start a new isolated container which immediately opens up an interactive terminal inside the container, this is determined by the presence of the `-it` switch in the `docker run` command.

By default, the interactive terminal that is opened is a `bash` shell, however if you prefer using `PowerShell` then thats fine, we have you covered as we also bundle `PowerShell 7` as part of the image. If you want to use PowerShell instead, simply add `pwsh` to then end of the `docker run` command and you will get a PowerShell session instead.

```
docker run --rm -it m365pnp/cli-microsoft365:latest pwsh
```

Now that you are at the interactive terminal, you can now invoke any CLI for Microsoft 365 command using the `m365` prefix as it is already installed, to help you, we have even pre-configured tab command completion for you in both `bash` and `PowerShell`. Neat right.

When you are done with your session, just type `exit` and your interactive terminal will be closed and with that, the isolated container will also be stopped and removed, freeing up resources on your host machine, this is determined by the presence of the `--rm` switch in the `docker run` command.

This doesn't mean that the image you just downloaded has been removed as well, this remains on your machine, we just removed the container instance that was started, so when you run the `docker run` command again, this time you won't need to download the image and just head straight for the interactive terminal.

Checkout our [guide](https://pnp.github.io/cli-microsoft365/user-guide/run-cli-in-docker-container/) for more details on how to use these images, including how to get the latest beta releases, update existing images and how to invoke scripts from your host machine inside the running container.

We will be releasing new beta and stable versions as part of our regular release cadence, so you will be able to use new version of the CLI in Docker immediately after our release to `npm`.
