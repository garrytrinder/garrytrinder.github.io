---
layout:         post
title:          Getting started with Office 365 CLI and PowerShell
category:       Office 365 CLI
tags:           [PowerShell, PowerShell Core, Office 365 CLI, PowerShell Core, pwsh]
permalink:      /:year/:month/:title
published:      true
---

In this post, we will show you how to get started with using the Office 365 CLI with the popular PowerShell scripting language on Windows and now also cross platform using PowerShell Core (`pwsh`).

### Why would I want to use the Office 365 CLI?

As more and more organisations move into Office 365, more solutions are being built that expand beyond the Windows operating system. Developers and adminstrators are no longer constrained to Microsoft development technologies tied to the Windows platform, opening up the possibility to develop applications and automation scripts using cross platform technologies to authenticate and communicate with Office 365 workloads.

Unfortunately, managing many of the workload settings is possible only through using PowerShell on Windows. It is typicaly for developers and administrators to use a combination of different PowerShell modules to achieve this, such as [PnP PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps) and [SharePoint Management Shell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/introduction-sharepoint-online-management-shell?view=sharepoint-ps). For non-Windows users to handle such a scenario, it is common for them to use Windows Virtual Machines just to manage these settings, which is not convenient and can be costly.

The [Office 365 CLI](https://github.com/pnp/office365-cli) is a cross-platform command line interface that enables you to manage your Office 365 tenant on any operating system or shell, whether you are on Windows, MacOS, or Linux, or use CMD, PowerShell, bash or zsh. 

The CLI also provides a single unified login to Office 365 workloads. It is becoming more and more common that you need to manage and provision assets in many different workloads in the same script and it is incovenient to connect/disconnect with them individually. The CLI handles this complexity for you, enabling you to concentrate on your script logic without having to handle the authentication requirements for each workload as this is managed behind the scenes for you.

### Installing the Office 365 CLI

> The CLI runs on NodeJS, therefore it does require that you have Node v6 or higher installed on your machine. 

Open up a PowerShell session and install the CLI using `npm`, once installed, this will be available to use in your shell.

```
PS > npm install @pnp/office365-cli -g
```

> Learn more about installing the Office 365 CLI [here](https://pnp.github.io/office365-cli/user-guide/installing-cli/)

### Setup command completion

One of the key features of PowerShell is that tabbed command completion is built in by default. If you want to find a command to use you can simply `tab` and move through the different cmdlets available to you.

With the 2.7 (March 2020) release of the Office 365 CLI, we added command completion functionality for PowerShell, to enable a similar experience when using the CLI.

To enable command completion, we have provided a command in the CLI to help do this for you.

Using the `cli completion pwsh setup` command adds a reference in your PowerShell profile which loads the CLI command completion when you open a new PowerShell session.

```
PS > o365 cli completion pwsh setup --profile $PROFILE
```

> Notice that we prefix the `cli completion pwsh setup` command with `o365` in the above example. To execute any CLI command using PowerShell, we must prefix them with `o365` or `office365` to access the CLI in non-immersive mode.
>
> Learn more about immersive and non-immersive mode [here](https://pnp.github.io/office365-cli/user-guide/using-cli/#start-the-cli).

You should close your current PowerShell session after running the above command for the changes to take effect.

When you next use the CLI commands, you can use `<tab>` to return options available to you, for example, `o365 <tab>` to return all top level command groups.

![](/public/img/o365cli/pwsh_command_completion.png){: .center-image }

> With every release of the Office 365 CLI, (beta releases are weekly and major releases are monthly), we add new commands for you to use.
>
>  To ensure that you can use these new commands in command completion, you need to update, to do that use the `update` command.
>
> ```
> PS > o365 cli completion pwsh update
> ```

#### View command help

In PowerShell, you can the `Get-Help` cmdlet to return interactive help for a given cmdlet as the Office 365 CLI is not built using PowerShell it is not possible to use this, however we do provide a `--help` option on all commands in the CLI. 

Use this to return information on what the command does, the options available and examples of how to use the command.

```
PS > o365 spo web get --help

  Usage: spo web get [options]

  Retrieve information about the specified site

  Options:

    --help                 output usage information
    -u, --webUrl <webUrl>  URL of the site for which to retrieve the information
    --query [query]        JMESPath query string. See http://jmespath.org/ for more information and examples
    -o, --output [output]  Output type. json|text. Default text
    --pretty               Prettifies json output
    --verbose              Runs command with verbose logging
    --debug                Runs command with debug logging

  Examples:
  
    Retrieve information about the site https://contoso.sharepoint.com/subsite
      spo web get --webUrl https://contoso.sharepoint.com/subsite
```

### Authenticating with your Office 365 tenant

Before we run any commands that call Office 365, we need to make sure that we are connected to our Office 365 tenant, you can do this using the `login` command.

```
PS > o365 login
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code XXXXXXXXXX to authenticate.
```

The default login method used is the device code method, this is ideal for using accounts that have multi-factor authentication enabled on them as the login is interactive and performed in the browser. 

Simply navigate to the Microsoft device login screen, enter the code returned from the command and login using your Office 365 account.

> Learn more information about authenticating with Office 365 CLI and other authentication methods available [here](https://pnp.github.io/office365-cli/user-guide/connecting-office-365/#log-in-to-office-365)

### Executing commands from PowerShell

Once connected to your Office 365 tenant, executing commands is straight forward. 

If we want to return information about a SharePoint Online site, we can use the `spo web get` command, as shown in the example below.

```
PS > o365 spo web get --webUrl "https://contoso.sharepoint.com"
Title : My Awesome Site
Url   : https://contoso.sharepoint.com
...
```

> Learn more about all the commands available [here](https://pnp.github.io/office365-cli/cmd/consent/)

### Working with data

In the previous example, the response is simply returned to the PowerShell prompt as text, however when building scripts we want to reuse information from previous commands to pass into other commands, or interrogate the returned responses in more detail.

To work with the data returned from the CLI commands, we can use `--output json` option to ask the CLI to return JSON instead of text, which is the default output type for all CLI commands, and  convert that response into it into a useable object.

PowerShell conveniently provides us with a cmdlet to do this, `ConvertFrom-Json`, which makes coverting JSON responses into a PowerShell object easy.

We can use a pipe (`|`) to pass the output of the CLI command directly to this cmdlet and save it as a PowerShell variable which enables us to then access properties directly and return their values.

If we want to access the Title property value of a SharePoint Web, building on the previous example we can use this approach, as shown in the example below.

```
PS > $web = o365 spo web get --webUrl "https://contoso.sharepoint.com" --output json | ConvertFrom-Json
PS > $web.Title
My Awesome Site
```

And if we wanted to iterate over a response that returns a JSON array we can pipe the PowerShell object into the `ForEach-Object` cmdlet, as shown in the example below.

```
$sites = o365 spo site list -o json | ConvertFrom-Json
$sites | ForEach-Object { $_.Title }
```

As the above examples show, we can easily create PowerShell objects using this approach using the `ConvertFrom-Json` cmdlet and the use the data with any PowerShell cmdlet available.

> **Example Scripts**
>
> The Office 365 CLI web site contains a section for example scripts, with many using PowerShell.
>
> Checkout the examples [here](https://pnp.github.io/office365-cli/examples/). 
> 
> If you build a script and would like to add it our examples section, we would love to hear from you, get in touch with the project our at our GitHub [repository](https://github.com/pnp/office365-cli).

### Find out more

If you need more help getting started or want more details about the commands, the architecture or the project, go to [https://aka.ms/o365cli](aka.ms/o365cli). 

If you see any room for improvement or suggestions, please don’t hesitate to reach out to us either on [GitHub](https://aka.ms/o365cli) or [@office365cli](https://twitter.com/office365cli) on Twitter.
