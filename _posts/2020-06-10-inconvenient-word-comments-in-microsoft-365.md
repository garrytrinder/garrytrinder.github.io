---
layout:         post
title:          Inconvenient Microsoft Word comments in Microsoft 365
category:       Microsoft 365
tags:           [Microsoft Word, Microsoft 365, Microsoft Teams]
permalink:      /:year/:month/:title
published:      true
---

I have been recently looking into how the comments feature in Microsoft Word works across Microsoft 365, specifically around the @ mention feature, to help customers be more productive when authoring and reviewing documents, however I noticed that it doesn't always work as you would maybe expect it to.

The Comments feature has been in Microsoft Word for a long time, so long that I'm pretty sure most of us just refer to it as always being there, it enables you to highlight a section of the document and make a comment, starting a discussion thread directly within that document, where others can reply, with the ultimate aim to provide feedback that can be actioned before publishing the document to wider audience.

As time has moved on this feature has been given an upgrade, as we now live in a more connected world, the ability to @ (at) mention was included so that you could notify colleagues directly in a comment to get their immediate feedback. It is a great feature, however as our world has got bigger, we now access our documents in different ways, through Microsoft Teams, the browser, desktop and mobile apps, which has led to some differences in the functionality offered which may have an impact on how you might choose to collaborate on a document with your colleagues.

So lets take a look at the two types of @ mentions possible...

_@ mentions in comments_, this is what most people will be used to doing, you create a new comment in the document and in the comment @ mention the person who you want to notify, sending an auto email to that person letting them know that something needs their attention. 

_inline @ mentions_, rather than creating the comment first and then @ mentioning, you can @ mention directly within the document. This automatically creates a comment with the comment of the person who you @ mentioned, whilst this can be useful, the comment that is auto-created is less than desirable as you have to explain what your comment is in a reply, this will send an auto email to that mentioned person.

There are a couple of features to be aware of that that are associated with the use of comments in Word...

_Follow-Ups_, is a view displayed in the Navigation pane which lists all the instances in the document where a person has been @ mentioned, useful for you to jump to different locations in a long document where your input is required.

_Share and Notify_, if you @ mention someone who does not have access to the document, a prompt will be displayed asking whether you would like to share that document with that person, this can be useful or not, depending on your situation.

## Word Online in Teams

Now that we know the features, lets see what functionality is available, starting with one of the most common scenarios at the moment, viewing a Word document via the Microsoft Teams interface. 

As this is going to be quite a common scenario, I was quite surprised to find that it is not possible to @ mention in a comment and you cannot @ mention inline, you do however get the Follow-Ups section in the Navigation pane. 

To compensate for the lack of @ mentions, as the document is being shown within the Teams interface, you do get the ability to create a teams conversation and @ mention people in the conversation but as this is outside of the document this conversation will not be visible to other authors or reviewers viewing the document outside of the Teams interface, it also doesn't allow you to highlight sections of the document, like you can with a comment, so could be problematic when using this approach to give context about a change that is required in a document. I see this as useful to talk around the document in general but not specific areas.

> Document conversations are created in the Channel closest to where that file is stored, for example, if the file is accessible from the Files tab on the General channel, the new conversation will be created in the Posts tab of the General channel.

## Microsoft 365 Word

After viewing the document in the Teams interface, chances are that most people will open the document in Microsoft Word desktop app using the 'Open in Desktop App' button. When viewing the document outside of the Teams interface, it is noticeable that a few options now change, Conversations are gone, @ mentions in comments are now possible but inline @ comments are not. 

We now have @ mentions, great, however there is something that you need to be careful of, if you @ mention a person who does not have access to the document i.e. not a member of the Team that the document is stored in, when you mention them, you will receive a prompt that tells you that this person does not have access to the document and that you can share the document with them and notify them that the document hsa been shared with them.

Whilst this is a nice feature, what this does behind the scenes is that it gives the person being mentioned edit access directly to the document. No problem, you might think, it is however worth knowing that when you grant access to a document this way you are using document level permissions which can make managing and tracking who has access to which document in the future difficult, as this is not easily noticeable which documents have unique permissions applied, you will have to look into the permissions in SharePoint to see who has access to the document. One ommision from the desktop app is the Follow-Ups view, if you have a few mentions in a document you will need to manually search for them.

> Note: Both the Windows and Mac OS versions of Word have the same functionality

## Word Online in Browser

Another way to view the document is to open the document in Word Online using the 'Open in Web Browser' button, whilst you would think that there won't be much difference between Word Online in the browser and Word Online in Teams, it is noticeable that a few options are not the same, Conversations are gone in the same way as in the desktop app, @ mentions in comments and inline @ mentions are now possible as and the Follow-Ups view is visible in the Navigation pane. Again, like in the desktop app, mentioning a person who does not have access to the document will give the Share & Notify prompt.

## Word for iOS (iPad)

Lastly, as more people are using the Word for iOS app on mobile and tablet, this supports does support @ mentions in comments and will prompt to Share & Notify if mentioning people who don't have access to the document, but inline @ mentions and the Follow-Ups view are not supported.

## Summary

I was quite surprised to see the difference in this functionality across the different versions of Word that could be used when authoring and reviewing a document across Microsoft 365. 

The one place where I would have expected @ mentions to work due to it being a common interface, is through the Teams interface but this is not the case, as it favours using the Conversations route instead for @ mentioning. The main reason for this seems to be to stop team members from sharing the documents directly with individuals outside of the Team without maybe realising it, however this can easily be done via other Word versions such as the desktop app.

The below table shows what functionality is available in different versions of Word in Microsoft 365.

|                                    | @ Comment | @ Inline | Follow-Ups | Conversations | Share & Notify |
| ---------------------------------- |:---------:|:--------:|:----------:|:------------:|:----------------:|
| Word Online in Teams               | ❌        | ❌        | ✅          | ✅            | ❌           |
| Word Online in Browser             | ✅        | ✅        | ✅          | ❌            | ✅           |
| Microsoft 365 Word                 | ✅        | ❌        | ❌          | ❌            | ✅           |
| Word for iOS (iPad)                | ✅        | ❌        | ❌          | ❌            | ✅           |