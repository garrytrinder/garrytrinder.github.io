---
layout:         post
title:          Export Time Entries from Harvest using Microsoft Flow
category:       Integration
tags:           [Microsoft Flow,Harvest,OpenAPI,Custom Connector,OAuth 2.0,PowerPlatform]
permalink:      /:year/:month/:title
published:      true
---

[Harvest](https://getharvest.com), we are big fans of the time recording system [@idlive](https://www.id-live.com) and have been using it for years to track time spent on delivering projects for our clients. After a discussion one day with our Delivery Lead, he expressed an idea... "wouldn't it be great if we could share the time tracked on our projects directly with our customers?". An idea was born and a solution was to present itself...

One Sunday afternoon I sat down to look at the first problem... "how do I export time entries out of Harvest?" which this post tackles.

Naturally my first port of call was Microsoft Flow. I knew that there are serveral standard Harvest connectors provided, unfortunately for time entries, you can only return a single entry by its ID and create a new entry, neither of which were really going to help me.

In this situation, when there is no standard way to integrate with a third party system, the best way is to create a Custom Connector to "fill in the gaps".

Harvest has a mature and well documented API, one of many reasons why its so good, so this was a fairly straight forward task to create a connector that securely calls the Harvest API to return time entries for all projects.

The action that I created, List all time entries, takes three parameters, the Harvest Account ID for the account you want to return data from (this is required for all requests), the date I wanted to return time entries from, (we have over 5 years worth of time entries so don't want them all) and a page number.

![](/public/img/flow/harvest-time-entries-getalltimeentries-action.png){: .center-image }

So great, I now have the ability to pull back time entries, job done... well, maybe not... you see, the Harvest API only returns 100 entries at a time (see [Pagination](https://help.getharvest.com/api-v2/introduction/overview/pagination), so I needed to come up with a way of how to loop through all of the pages.

Enter the 'Do Until' action, this allows us to repeat an series of actions until a certain condition is met, in this case I needed to keep calling the Harvest API but each time asking for the next page of results until the current page was higher than the total pages for my query.

![](/public/img/flow/harvest-time-entries-dountil.png){: .center-image }

Using a combination of variables to store the current page value (HarvestPage) and total pages value (HarvestTotalPages), I update these in the Do Until loop using the Increment Variable and Set Variable actions respectively.

![](/public/img/flow/harvest-time-entries-variables-update.png){: .center-image }

So now I have worked out how to call the Harvest API securely and being able loop through all the pages of time entries. I now needed to be able to store the response from each API call to build up a single collection of all the time entries I need.

The way to do this was to initialize an Array variable (HarvestTimeEntries) and by using a Compose action within the Do Until loop, I use the Union() function to merge the two Arrays into one, the initially empty, HarvestTimeEntries variable and the response from the latest Harvest API call.

![](/public/img/flow/harvest-time-entries-union.png){: .center-image }

Great, so I have all the time entries I need in one place but now I need to be able to store in a place where it can be reported on.

This next step would involve storing each time entry returned in Azure SQL. Now you would think that this again would be something that Flow can do easily, which it can, but with a downside... its very slow. 

Looping through all the time entry objects in the HarvestTimeEntries array and using the Insert Record SQL Server action took an absolute eternity to finish. Flow is really poor at handling large iterations, we are talking thousands of rows here, so it wasn't a great solution and there had to be a better way... which there is... 

I will follow up with another blog post of how I import thousands of records stored in JSON format, directly into Azure SQL Server in a matter of seconds by using a single action in Flow.

The Harvest API Custom Connector that I use in this Flow is on Github [here](https://github.com/garrytrinder/harvest-api-powerplatform-custom-connector), with instructions on how to setup the connector in your own tenant.

### Complete Flow

![](/public/img/flow/harvest-connector-time-entries.png){: .center-image }

