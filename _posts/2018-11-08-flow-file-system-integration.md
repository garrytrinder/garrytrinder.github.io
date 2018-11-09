---
layout:         post
title:          Flow loves Legacy Systems
category:       Flow
tags:           [Flow,Integration,Legacy,File System]
permalink:      /:year/:month/:title
published:      true
---

Legacy systems... yes, you know the ones... where an API is a collection of folders where flat files are picked up by scheduled tasks import tasks... no web APIs here... built using old technologies and running on a server in the corner of the office. This is far removed from cloud computing, but it doesn't mean that it can't make use of what the cloud has to offer.

We recently took on a project with a customer who had one of these legacy systems, the system is used heavily within their business to manage the day to day operations of their maintenance engineers as well as invoicing, so quite important, abeit old, it still delivers business value.

We have been brought in to help modernise the way that there maintenance engineers send updates to the back office team, who have the task of importing these updates into the system using a combination of Excel spreadsheets and flat files. Not the quickest or easiest of processes to deal with, but it works to a degree.

As part of our modernisation, we are building a PowerApp that will allow the maintenance engineers to remotely view the jobs they need to carry out and also complete them, removing them from their task list whilst also updating the legacy system so that a job can be invoiced. Simple right...

Well, not so much, remember this is a legacy system, it doesn't have a web api that we can just call and get an instant response, it uses flat files and we have the small problem of getting this data from the cloud onto the server in the corner of the office, oh and we have no way of knowing whether the file we just dropped on to the server has been sucessful or not, remember we don't get an instant response.

The good news is Flow can help handle all of this and quite easily... yay!

So the first thing to do was to setup the Data Gateway, this is what allows us to connect to our local server in Flow and using it in conjunction with the File System action, we can move files using Flow into a destination folder on the server ready for importing.

Great, but we still have to generate the file that includes the updates from the maintenance engineer, in our case, this is a tabbed delimited file, just to add another layer of complication.

Using a SharePoint Document Library to store a template import file, we can use the SharePoint Get File Content action, as we need to send over different information we use tokens that we can then update using a series of Compose actions so that we end up with a file that is complete and has the information that we need.

We then take that file and drop it on the server using the File System Create File action, as well as dropping the same file into another SharePoint Document Library so that we have a place where we track the files that we have sent and when.

The import process of the legacy system is a simple one, drop the file into a process folder, if it works, it is dropped into a success folder, if it fails, it well you get the idea... so we can reuse the File System triggers to check for new files in a specific location. 

We have built two flows that trigger on a new file entering the success and failure folders respectively, which we can then use to notify invoicing of a new completed job or notify someone to investigate why the import failed.

In all, the integration side of the project has taken very little time to implement, literally hours, which I find amazing.

In years gone by this level of integration would have resorted to writing code and would have taken days, even weeks, to achieve. 

Flow has taken all that pain away and given much more flexibility to what traditionally has been rigid, costly exercise.

So if you have old systems, don't think that they can't have their day once again, Flow can help :)









