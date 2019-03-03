---
layout:         post
title:          Removing unnecessary Apply to Each action when using Get Items action
category:       Integration
tags:           [Microsoft Flow,SharePoint,Get Items, Performance, Expression, Refactoring, First()]
permalink:      /:year/:month/:title
published:      true
---

Flow is great, but it can add unnecessary Apply to Each actions which can slow you down and clutter your Flows but using an Expression can help.

Whilst working on Flows to automate business processes for clients, I'm always looking for ways that I can streamline them, removing actions that appear unnecessary but are easy to add to your Flow sometimes without you realising.

One of those cases is you use the SharePoint Get Items action, being a SharePoint guy I use this action alot, usually to query a list to return a single item based on some identifier that is not the Item ID, such as a unique Title.

> Get Items action will always return an Array of Items even if you only want one Item

The response from this action will always return an array of SharePoint list items, even if you specify 1 in the Top property of the action, telling the action that you are only interested in one item.

In future steps if you add a property from this action into another action, that action is automatically placed in an "Apply to Each" action, just for a single item.

The example below shows how this happens, we are getting a single car from a list of Cars and using it in the next action.

![](/public/img/flow/getitems-applytoeach.jpg){: .center-image }

Creating a loop for a single item is an unnecessary overhead, it would be better to just access the first item directly without the loop. 

This is where an Expression and the First() function comes in, allowing us to remove the Apply to Each from the Flow.

![](/public/img/flow/getitems-first.jpg){: .center-image }

The expression used above is in full below

``` javascript
first(body('Get_Car_from_Cars_List')?['value'])?['Manufacturer']
```

 > body references are always the name of the actions but spaces replaced with underscores. Name your actions wisely!

Although this is a very simple example, when we are building Flows it is quite easy for them to become large quite quickly so any way of removing actions is a good thing.

References

[Workflow Definition Language functions reference for Azure Logic Apps](https://docs.microsoft.com/en-us/azure/logic-apps/workflow-definition-language-functions-reference)