---
layout:         post
title:          Identify SharePoint Online Site Experience by PowerShell
category:       Administration
tags:           [PowerShell,SharePoint,Modern SharePoint,Classic SharePoint,SharePoint Online,'#sphelp',Site Templates]
permalink:      /:year/:month/:title
published:      true
---

We live in a world where SharePoint has become somewhat of a split personality, we have the Modern experience and the Classic experience, confusing for end users but also difficult for administrators to track.

I had some spare time this weekend and noticed this tweet on the #sphelp hashtag.

<blockquote class="twitter-tweet tw-align-center" data-partner="tweetdeck"><p lang="en" dir="ltr">SharePoint Online PowerShell question: Is there a way to pull a list of sites with a property for classic or modern? <a href="https://twitter.com/hashtag/SPHelp?src=hash&amp;ref_src=twsrc%5Etfw">#SPHelp</a> <a href="https://twitter.com/ciphertxt?ref_src=twsrc%5Etfw">@ciphertxt</a> <a href="https://twitter.com/PlateSpinner?ref_src=twsrc%5Etfw">@PlateSpinner</a> <a href="https://twitter.com/ToddKlindt?ref_src=twsrc%5Etfw">@ToddKlindt</a> <a href="https://twitter.com/O365Adam?ref_src=twsrc%5Etfw">@O365Adam</a></p>&mdash; Sam Larko (@SPSamL) <a href="https://twitter.com/SPSamL/status/1073473591440826369?ref_src=twsrc%5Etfw">December 14, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

So thought I'd take a look, the result of which was this script.

<script src="https://gist.github.com/garrytrinder/358b8cb06e2b41c980a4d48abce52390.js"></script>

Which gives you the below output.

![](/public/img/powershell/get-spositetemplateexperience-output.png){: .center-image }

It uses the Microsoft.Online.SharePoint.PowerShell model to return all SharePoint Online sites using Get-SPOSite for a connected tenant and using an expression column, it determines whether the site is modern or not based on its template.

The list of templates (to my knowledge) that determine a modern site are

| Template             | Description                                      |
| :------------------- | :----------------------------------------------- |
| STS#3                | Modern Team Site with No Office 365 Group        |
| GROUP#0              | Modern Team Site with Connected Office 365 Group |
| SITEPAGEPUBLISHING#0 | Modern Communications Site                       |

A good starting point if nothing else to track down those classic sites or just to see how much spread of site experiences you have across your tenant 😀