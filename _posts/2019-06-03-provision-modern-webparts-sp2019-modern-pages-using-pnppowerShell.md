---
layout:         post
title:          Provision modern webparts on SP2019 modern pages using PnP PowerShell
category:       Provisioning
tags:           [SharePoint,On Prem,SP2019,Modern,SPFX,PnP,PowerShell]
permalink:      /:year/:month/:title
published:      true
---

🚨 UPDATE 🚨 You can now use Add-PnPClientSideWebPart cmdlet as it is now enabled for use in the SharePoint Server 2019 PnP PowerShell [module](https://github.com/SharePoint/PnP-PowerShell/pull/2250).

~~PnP PowerShell is my go to for automating most things in SharePoint, whether that is the Online or On Prem flavours. However there are times when there is a specific cmdlet only available in SharePoint Online, I recently came across this whilst working on a SharePoint 2019 project using the Modern page experience and SharePoint framework.~~

~~Add-PnPClientSideWebPart is only available for SharePoint Online, so I had to get creative. The below script will enable you to add 3rd Party or out of the box modern web parts for a modern client side page, using the same usage as the Online cmdlet.~~

<script src="https://gist.github.com/garrytrinder/c159da607848c714b8c98c5459f402b7.js"></script>
