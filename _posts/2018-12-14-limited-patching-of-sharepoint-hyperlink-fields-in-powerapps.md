---
layout:         post
title:          Limited patching of SharePoint Hyperlink fields in PowerApps
category:       PowerApps
tags:           [PowerApps,SharePoint,Hyperlinks,Patch]
permalink:      /:year/:month/:title
published:      true
---

PowerApps and SharePoint have a strange relationship, on one hand they work great together for simple things, but sometimes they just don't get along in the way you would expect.

A colleague who was working on an app we are building for a client was having issues updating the hyperlink field, his actually issue was more around passing the value of a textbox which happened to be a number not text, but the issue was raised.

I was busy at the time so threw out a tweet to get some traction on solving the issue whilst mentioning some well known PowerAppers in the process.

<div style="text-align:-webkit-center"><blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">Anyone know if it is possible to update a SharePoint Hyperlink field using Patch() in <a href="https://twitter.com/PowerApps?ref_src=twsrc%5Etfw">@PowerApps</a> ? <a href="https://twitter.com/ShanesCows?ref_src=twsrc%5Etfw">@ShanesCows</a> <a href="https://twitter.com/8bitclassroom?ref_src=twsrc%5Etfw">@8bitclassroom</a> <a href="https://twitter.com/hashtag/PowerAppsHelp?src=hash&amp;ref_src=twsrc%5Etfw">#PowerAppsHelp</a></p>&mdash; Garry Trinder (@garrytrinder) <a href="https://twitter.com/garrytrinder/status/1073581191410929664?ref_src=twsrc%5Etfw">December 14, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script></div>

Shane thankfully replied and helped push me in the right direction but gave me confidence that it was indeed possible.

<div style="text-align:-webkit-center"><blockquote class="twitter-tweet" data-conversation="none" data-cards="hidden" data-partner="tweetdeck"><p lang="en" dir="ltr">If I remember correctly you can update either the URL or the text but not both? Make a sample app with the Hyperlink column and see what options it offers you. Good place to start.</p>&mdash; Shane Young PowerApps MVP (@ShanesCows) <a href="https://twitter.com/ShanesCows/status/1073585537460699136?ref_src=twsrc%5Etfw">December 14, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script></div>

So I did exactly that, built a PowerApp and tested it myself.

As a SharePoint guy of many years, I know that a Hyperlink field is made up of two parts, Description and Url, the Description being the display text of the link when displayed in a SharePoint list and the Url, the target of the link.

However, it appears that PowerApps does not, it only knows half the truth, the Url.

Take the patch below, it creates an item in a SharePoint list with the Hyperlink field set to a location on Google Maps...

![](/public/img/powerapps/patch-hyperlink.png){: .center-image }

... but it updates both the Url and Description property to the same value that is passed in.

![](/public/img/powerapps/patch-hyperlink-listitem.png){: .center-image }

To try and solve this, I've tried the old SharePoint tricks of formatting the string passed in the Patch in particular format, some of them I've tried below.

 -  {url};#{text}
 -  {url}, {text}
 -  {url},{text}
 -  {url};{text}

 None of them updated the Description, it just saved the full string in the Url field, breaking the link.

Investigating more on this, I looked at how a NewForm would treat a Hyperlink field, and it treats it in the same way, you just get a single field and there is no way of updating both the Url and Description independantly of each other.

For our scenario, we could handle the fact that we couldn't update the Description but it worth knowing that this isn't possible in PowerApps yet. 

The only way that I think you could do this is by using a Flow which uses the SharePoint HTTP action to update the item using the REST API or by creating a Custom Connector, but as Beau Cameron points out below, there are license considerations to be made.

<div style="text-align:-webkit-center"><blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">Ya, just be aware of the Flow and PowerApps licensing changes coming if you go that route...</p>&mdash; Beau Cameron (@Beau__Cameron) <a href="https://twitter.com/Beau__Cameron/status/1073587580166258688?ref_src=twsrc%5Etfw">December 14, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script></div>

Big thanks to Beau for giving me the push to post this and help get over my blog post anxiety, cheers buddy 😊👍🏻