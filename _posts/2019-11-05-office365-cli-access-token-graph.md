---
layout:         post
title:          Easily authenticate with and call the Microsoft Graph using Office 365 CLI and PowerShell Core 
category:       Development
tags:           [Microsoft Graph,Office 365 CLI,PowerShell Core]
permalink:      /:year/:month/:title
published:      true
---

This post will show you how you can easily authenticate with and call the Microsoft Graph using using Office 365 CLI and PowerShell Core. 

<script src="https://gist.github.com/garrytrinder/0e606d2c3e48ddc4bf36b502ac884cff.js"></script>

We start by entering a PowerShell Core interactive session using `pwsh -NoLogo`, the `-NoLogo` switch hides the copyright banner at startup.

Once into the pwsh session, we authenticate with Office 365 using the `login` command in the Office 365 CLI. This command will initiate the device login process as default however this can be changed to use a specific username and password or certificate, if required.

Once authenticated, we use the `accesstoken get` command to return a new access token specifically for the Microsoft Graph, the Uri of which is passed in as the value of the resource parameter, `-r https://graph.microsoft.com`.

Now that we have our access token, we can pass this into the `Authorization` header of a HTTP request as a `Bearer` token, the request is invoked by the `Invoke-WebRequest` cmdlet which performs a GET request to the Uri of a Microsoft Graph endpoint, which in this example is the `me` endpoint which returns information about the currently logged on user.

The HTTP response is returned as an object containing the JSON response which is contained in the Content property of the repsonse. We parse the response content to create a PowerShell Object from the returned JSON using the `ConvertFrom-Json` cmdlet that we can then inspect. Easy!

![](/public/img/powershell/o365-cli-pwsh-graph.png){: .center-image }

Although this example uses the Microsoft Graph, we can use this same approach to return access tokens for other services. For example, we could pass `https://tenant.sharepoint.com` as the value of the resource parameter when invokeing the `accesstoken get` command to return an access token for a SharePoint Online tenant instead.

> This post was inspired by a demo presented by Lee Ford ([@lee_ford](https://twitter.com/lee_ford)) at the Global Microsoft 365 Developer Bootcamp held in Nottingham, where he demonstrated how he used PowerShell Core to call the Microsoft Graph. This post simplifies the authentication by using the Office 365 CLI. Thanks Lee 👍🏻

### More information

 - [Microsoft Graph](https://developer.microsoft.com/en-us/graph/)
 - [Office 365 CLI](https://pnp.github.io/office365-cli)
   - [login](https://pnp.github.io/office365-cli/cmd/login/)
   - [accesstoken get](https://pnp.github.io/office365-cli/cmd/accesstoken-get/)
 - [PowerShell Core](https://docs.microsoft.com/en-gb/powershell/scripting/overview?view=powershell-6)
   - [Invoke-WebRequest](https://docs.microsoft.com/en-gb/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-6)
   - [ConvertFrom-Json](https://docs.microsoft.com/en-gb/powershell/module/Microsoft.PowerShell.Utility/ConvertFrom-Json?view=powershell-6)
