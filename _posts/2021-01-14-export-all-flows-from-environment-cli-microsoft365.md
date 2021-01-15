---
layout:         post
title:          Export all your Power Automate Flows using CLI for Microsoft 365
category:       Automation
tags:           [cli,microsoft356,powershell,backup,export,power,automate,power,platform,flows,flow]
permalink:      /:year/:month/:title
published:      true
---

When was the last time you backed up all the Flows in your environment?

By combining the [CLI for Microsoft 365](https://pnp.github.io/cli-microsoft365) and PowerShell we can make this task easy and repeatable.

This script will get all Flows in your default environment and export them as both a ZIP file for importing back into Power Automate and as a JSON file for importing into Azure as an Azure Logic App.

> The script assumes that you have already logged into your Microsoft 365 tenant using the `m365 login` command. 
> 
> See [Logging in to Microsoft 365](https://pnp.github.io/cli-microsoft365/user-guide/connecting-office-365/) in the user guide.

<script src="https://gist.github.com/garrytrinder/2f860630b8ef3945954ca922cb99cefc.js"></script>

> CLI for Microsoft 365 is associated with the [Microsoft 365 Patterns and Practices](https://pnp.github.io) (PnP) organisation, which is a virtual team consisting of Microsoft employees and community members focused on helping the community make the best use of Microsoft products.