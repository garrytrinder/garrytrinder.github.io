---
layout:         post
title:          Flow ❤️ Legacy Systems
category:       Integration
tags:           [Microsoft Flow,Legacy,File System,On-premises data gateway, SharePoint Online,]
permalink:      /:year/:month/:title
published:      true
---

Legacy systems... yes, you know the ones... where an API is a collection of folders where flat files are picked up by scheduled tasks import tasks... no web APIs here... built using old technologies and running on a server in the corner of the office. This is far removed from cloud computing, but it doesn't mean that it can't make use of what the cloud has to offer.

We recently took on a project with a customer who had one of these legacy systems, the system is used heavily within their business to manage the day to day operations of their maintenance engineers as well as invoicing, so quite important, abeit old, it still delivers business value.

We have been brought in to help modernise the way that there maintenance engineers send updates to the back office team, who have the task of importing these updates into the system using a combination of Excel spreadsheets and flat files. Not the quickest or easiest of processes to deal with, but it works to a degree.

As part of our modernisation, we are building a PowerApp that will allow the maintenance engineers to remotely view the jobs they need to carry out, complete them and have the ability to create new jobs adhoc, all whilst updating the legacy system. Easy right...

Well, not so much, remember this is a legacy system, it doesn't have a web API that we can just call and get an instant response, it uses flat files and we have the small problem of getting this data from the cloud onto the server sat in the corner of the office, oh and we have no way of knowing whether the file we just dropped on to the server has been sucessful or not, remember we don't get an instant response.

The good news is Flow can help handle all of this and quite easily...

The first step was to setup the [On-premises Data Gateway](https://docs.microsoft.com/en-us/power-bi/service-gateway-onprem), this is what allows us to connect to our local server in Flow and using it in conjunction with the [File System connector](https://emea.flow.microsoft.com/en-us/connectors/shared_filesystem/file-system/), we can move files using into a destination folder on the server ready for importing.

Using a SharePoint Document Library to store a template import file, we get raw text content using the SharePoint Get File Content action. The template contains a number of tokens for us to replace with our own values using a series of Compose actions and the replace expression. Each compose action uses the previous action output so that at the end we have a a text file that resembles what we need to send to the server for import.

![](/public/img/flow/replace-tokens.png){: .center-image }

We take that file and drop it on the server using the File System Create File action, as well as dropping the same file into another SharePoint Document Library so that we have a place where we track the files that we have sent and when.

![](/public/img/flow/legacy-system.png){: .center-image }

The import process of the legacy system is a simple one, drop the file into a process folder, if it works, it is dropped into a success folder, if it fails, it well you get the idea... so we can reuse the File System triggers to check for new files in a specific location.

We have built two flows that again use the File System connector to trigger when a new file is added to the success and failure folders respectively, we can then use this to notify invoicing of a new completed job or notify someone to investigate why the import failed.

In all, the integration side of the project has taken very little time to implement, literally hours, which I find amazing. In years gone by this level of integration would have resorted to writing code and would have taken days, even weeks, to achieve. Flow has taken all that pain away and given much more flexibility to what traditionally has been rigid, costly exercise.

So if you have old systems, don't think that they can't have their day once again, Flow can help 😀