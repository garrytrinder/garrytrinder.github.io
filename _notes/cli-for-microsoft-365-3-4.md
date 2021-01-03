# CLI for Microsoft 365 v3.4

We’ve just published a new version of the CLI for Microsoft 365 with new commands for working with and managing Microsoft 365 tenants and SharePoint Framework projects on any platform.

## Manage Microsoft 365 and SharePoint Framework projects on any platform

CLI for Microsoft 365 is a cross-platform CLI that allows you to manage various configuration settings of Microsoft 365 and SharePoint Framework projects no matter which operating system or shell you use.

While building solutions for Microsoft 365 expands beyond the Windows operating system, managing many of the platform settings is possible only through PowerShell on Windows. As more and more users work on non-Windows machines, it’s inconvenient for them to have to use a Windows virtual machine to configure their tenants. With the CLI for Microsoft 365, you can configure your tenant no matter which operating system you use. Additionally, using CLI for Microsoft 365, you can manage your SharePoint Framework projects.

## New version of CLI for Microsoft 365 – v3.4

Following our monthly release cadence, we’ve released a new version of the CLI for Microsoft 365 with some new capabilities. Here are a few of the most noteworthy additions.

## Changes

We’ve continued improving CLI building upon the changes we’ve introduced in the previous version.

### Improved support for login with certificate authentication

The CLI supports a number of different authentication methods supporting user and app-only authentication scenarios, in automation scenarios it is quite common for certificate authentication to be used as a preference to using usernames and passwords, with that in mind we have made a number of improvements to the way that we handle certificate authentication by extending the `m365 login` command.

Previously, we only supported passing certificates as a file path to the `m365 login` command using the `--certificateFile` option, in the latest release we now support passing the contents of a certificate as a Base64 encoded string, this helps simplify scenarios where it is inconvenient to store certificates on disk such as in a CI\CD pipeline.

To pass a certificate as a Base64 encoded string, execute:

```
m365 login --authType certificate --certificateBase64Encoded MIII2QIBAzCCCJ8GCSqGSIb3DQEHAaCCCJAEg...eX1N5AgIIAA== --thumbprint D0C9B442DE249F55D10CDA1A2418952DC7D407A3
```

Previously, we asked for you to provide the certificate thumbprint along with the location of the certificate file, as in the example above, this is no longer required, we will now automatically calculate the thumbprint from the certificate passed in.

To have the certificate thumbprint automatically calculated for you, execute:

```
m365 login --authType certificate --certificateBase64Encoded MIII2QIBAzCCCJ8GCSqGSIb3DQEHAaCCCJAEg...eX1N5AgIIAA==
```

Previously, we asked for you to provide a password when using `.pfx` certificates, in the latest release, we have made the `--password` option optional. As it is possible to generate `.pfx` certificates with empty passwords, this is not mandatory and can be inconvenient when using certificates to authenticate against Microsoft 365 development environments.

> We always recommend that certificates used in production scenarios use a strong password

To use a `.pfx` certificate that uses an empty password, execute: 

```
m365 login --authType certificate --certificateFile /Users/user/dev/localhost.pfx
```

### Simplified usage of custom Azure Active Directory identities

In the past, if you wanted to [use your own Azure AD identity](https://pnp.github.io/cli-microsoft365/user-guide/using-own-identity/), we asked you to set the value of two environment variables, `CLIMICROSOFT365_AADAPPID` & `CLIMICROSOFT365_TENANT` to instruct the CLI to use your own Azure AD identity to authenticate with your Microsoft 365 tenant.

To simplify this process, we have introduced two new options to the `m365 login` command, `appId` and `tenant`, to instruct the CLI to use your own identity.

```
m365 login --appId 31359c7f-bd7e-475c-86db-fdb8c937548c --tenant 31359c7f-bd7e-475c-86db-fdb8c937548a
```

### Run CLI for Microsoft 365 in Docker Container

We recently [announced](https://developer.microsoft.com/en-us/office/blogs/run-cli-microsoft-365-in-docker/) that we are now publishing pre-configured Docker images to Docker Hub to make it easier for you to use the CLI. We will be releasing new beta and stable versions as part of our regular release cadence, so you will be able to use new Docker images immediately after our release to npm.

To run the latest version of the CLI in a Docker container, execute:

```
docker run --rm -it m365pnp/cli-microsoft365:latest
```

The Docker images are pre-configured with

- node@14
- bash
- PowerShell 7
- Command auto-completion
- Azure DevOps agent support

Checkout our [guide](https://pnp.github.io/cli-microsoft365/user-guide/run-cli-in-docker-container/) for more details on how to use these images, including how to get the latest beta releases, update existing images, execute scripts stored on your local machine inside the running container and how to use your own Azure AD identity for connecting to Microsoft 365 from the running container.

### Improved performance

We have made a couple of changes to the internal workings of the CLI to help improve performance of commands executed at the command line, these include improved lazy loading of dependencies so that we only load them when needed and we the `started` telemetry event, this event was primarily used to track when immersive mode was invoked and as you may remember we removed the immersive mode in v3, so this was no longer serving a purpose but was invoked if you executed `m365` to display the CLI interactive help.

## New Commands

### Set the default content type for a SharePoint Online list

By default, SharePoint includes many content types. Every piece of content in SharePoint is created from a content type. You can use the pre-defined content types, such as Blank Document or Announcement, without any change, or you can create custom content types. We've introduced a command that enables you to set the default content type on a list.

To set a content type with ID 0x0120 as default in the list with ID 0cd891ef-afce-4e55-b836-fce03286cccf located in site https://contoso.sharepoint.com/sites/project-x, execute:

```
m365 spo list contenttype default set --webUrl https://contoso.sharepoint.com/sites/project-x --listId 0cd891ef-afce-4e55-b836-fce03286cccf --contentTypeId 0x0120
```

### Get details about Microsoft Teams Direct Routing calls made within a given time period

Direct Routing allows you to make and receive calls whilst using an existing telephone provider through the Microsoft Teams interface, we've introduced a command to help your report on the usage of this method of calling.

To get details about Direct Routing calls made and received between 2020-10-31 and today, execute:

```
m365 teams report directroutingcalls --fromDateTime 2020-10-31
```

### Get details about Microsoft Teams PSTN calls made within a given time period

Public Switched Telephone Network (PSTN) calling can be configured to make and receive calls whilst using an existing telephone provider through the Microsoft Teams interface, we've introduced a command to help your report on the usage of this method of calling.

To get details about PSTN calls made and received between 2020-10-31 and today, execute:

```
m365 teams report pstncalls --fromDateTime 2020-10-31
```

### Search Yammer messages, users, topics and groups

Staying connected is more important than ever, Yammer is a social networking tool to openly connect and engage with employees across your organization. We have introduced a command to enable you to execute search queries across your Yammer network.

To returns search results for the query `community`, execute:

```
m365 yammer search --queryText "community"
```

To return a list of `groups` that match `community`, execute:

```
m365 yammer search --queryText "community" --show "groups"
```

to return a list of `topics` that match `community`, execute:

```
m365 yammer search --queryText "community" --show "topics"
```

To return a list of the first 50 `users` who match the search query `nuborocks.onmicrosoft.com`, execute:

```
m365 yammer search --queryText "nuborocks.onmicrosoft.com" --show "users" --limit 50
```

## New script samples

CLI for Microsoft 365 is a great tool both for quick adjustments to the configuration of your Microsoft 365 tenant as well as automating more complex tasks. Because CLI for Microsoft 365 is cross-platform you can use it on any OS and in any shell. To help you get started using the CLI for Microsoft 365 for automation scenarios, we started gathering some [sample scripts](https://pnp.github.io/cli-microsoft365/sample-scripts/).

> If you have any scripts that you use frequently, please [share](https://github.com/pnp/cli-microsoft365/issues) them with us so that we can learn more about the common automation scenarios.

## Contributors

This release wouldn’t be possible without the help of (in alphabetical order) 

 - [Patrick Lamber](https://github.com/plamber)
 - [Lee Ford](https://github.com/leeford)
 - [Waldek Mastykarz](https://github.com/waldekmastykarz)
 - [Nanddeep Nachan](https://github.com/nanddeepn)
 - [Yannick Reekmans ](https://github.com/YannickRe)
 - [Elio Struyf](https://github.com/estruyf)
 - [Garry Trinder](https://github.com/garrytrinder/)
 
Thank you all for the time you chose to spend on the CLI for Microsoft 365 and your help to advance it!

## Work in progress

Here are some things that we’re currently working on.

### More commands, what else

Microsoft 365 is evolving and new capabilities are being released every day. With CLI for Microsoft 365, we aim to help you manage your tenant on any platform in a consistent way, no matter which part of Microsoft 365 you interact with. While we keep adding new commands to CLI for Microsoft 365 each release, we still barely scratched the surface with what’s possible in Microsoft 365. In the upcoming versions of the CLI for Microsoft, you can expect us to add more commands across the different workloads in Microsoft 365.

### Friendlier commands

While there are now over 350 commands available to use in CLI for Microsoft 365 to help you manage your Microsoft 365 tenant, a lot of commands expect you to provide object ids to perform actions.

We understand that this is not as intuitive as being able to provide a the name of an object and the command work out what the required object ids for you based on the object name given.

We are actively creating new issues to address this, updating our commands to be more user friendly and provide a better user experience.

We’ll start to implement new name options on our Microsoft Teams commands and will start to appear in the next release.

Another thing that we’re working on in the context of simplification is allowing you to easily register applications in Azure AD. Creating Azure AD applications is a prerequisite in developing on Microsoft 365. We believe, that being able to do it with just one command would significantly improve the development process.

### Quicker and easier developer onboarding

CLI for Microsoft 365 is a community project and it relies upon contributions from developers around the world to help add new commands and enhance existing commands in every release.

As part of our ongoing improvements to the project, we want to make the onboarding process of new developers to the project as quick and easy as possible.

We will be looking to release a Remote Development container, that will provide a one click approach for developers to configure a development environment with all dependencies and tools required to contribute to the project.

The release will also support use of GitHub Codespaces, enabling developers to spin up dedicated development environments in the cloud and contribute to the project using nothing but a web browser.

### Script examples

In every release of the CLI for Microsoft 365, we introduce new commands for managing Microsoft 365. With 360 commands across the different Microsoft 365 services, the CLI for Microsoft 365 has become a powerful tool, not just for managing your tenant but also for automating your daily work.

We’d love to show you how you can use the CLI for Microsoft 365 to build automation scripts in PowerShell Core and Bash. If you have any scripts using SPO or PnP PowerShell that you use frequently, please share them with us so that we can learn more about the common automation scenarios.

### `ensure` commands

Currently, CLI for Microsoft 365 has dedicated commands for retrieving, creating and updating resources. If you were to create a script that ensures a specific configuration, for each resource you’d need to see if it exists, create it if it doesn’t or update it if it does.

We’re thinking about simplifying this scenario by introducing commands with a new verb named ensure. For example, to ensure that a particular site collection exists, instead of executing a combination of spo site list/spo site get, spo site add and spo site set, you’d execute spo site ensure with the necessary parameters which would automatically verify if the particular site exists and matches your configuration. If the site doesn’t exist, it would create it. If it does, the command would check if the properties you specified match the retrieved site and update them if necessary.

We’ll start to implement this idea on the spo site commands. We’d love to hear from you if it’s something that you’d find helpful and what other objects we should take into account.

## Try it today

Get the latest release of the CLI for Microsoft 365 from npm by executing in the command line:

`npm i -g @pnp/cli-microsoft365`

Alternatively, you can get the latest release from Docker by executing in the command line:

`docker run --rm -it @m365pnp/cli-microsoft365:latest`

If you need more help getting started or want more details about the commands, the architecture or the project, go to [aka.ms/cli-m365](aka.ms/cli-m365). 

If you see any room for improvement, please, don’t hesitate to reach out to us either on [GitHub](https://github.co/pnp/cli-microsoft365) or [twitter](https://twitter.com/climicrosoft365).