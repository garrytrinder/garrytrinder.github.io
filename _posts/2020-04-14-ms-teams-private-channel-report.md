---
layout:         post
title:          Identify and report on Microsoft Teams Private Channels using Office 365 CLI and PowerShell
category:       Microsoft Teams
tags:           [PowerShell, PowerShell Core, Office 365 CLI, PowerShell Core, pwsh, Microsoft Teams,Private Channels, Report]
permalink:      /:year/:month/:title
published:      true
---

Do you need to identify Microsoft Teams Private Channels in your tenant quickly?

When a Private Channel is created in a Microsoft Team, a new SharePoint site collection is created behind the scenes, however these are not visible in the SharePoint Online Admin Center (modern and classic) or easily identifiable in the Teams Admin Center, so it is useful from an adminstration point of view to be able to identify these.

Thankfully these sites are created using a site template called `TEAMCHANNEL#0` which we can use to track them down with.

The below script uses the `spo site classic list` command in [Office 365 CLI](https://aka.ms/o365cli) and PowerShells `Export-Csv` cmdlet, to identify those Private Channel sites and export some basic information about them into a CSV file.

> This script assumes you are already logged into your Office 365 tenant after using the `o365 login` command. [More](https://pnp.github.io/office365-cli/cmd/login/)

``` powershell
o365 spo site classic list -o json --query 'sort_by([], &Title)[?Template==`TEAMCHANNEL#0`].{Title:Title,Url:Url,Owner:Owner,Template:Template}' | ConvertFrom-Json | Export-Csv -NoClobber -Encoding utf8 -UseQuotes Always -Path teams-private-channel-report.csv
```

Which returns the below output

```
"Title","Url","Owner","Template"
"Sales and Marketing - Private Team","https://m365x835955.sharepoint.com/sites/SalesAndMarketing-PrivateTeam","meganb@m365x835955.onmicrosoft.com","TEAMCHANNEL#0"
...
```