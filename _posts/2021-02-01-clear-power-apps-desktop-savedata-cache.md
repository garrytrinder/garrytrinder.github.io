---
layout:         post
title:          Clear Power Apps Desktop SaveData cache
category:       Power Apps
tags:           [power apps,power platform,savedata,cache,clear,sharepoint,dataverse]
permalink:      /:year/:month/:title
published:      true
---

Since the start of the year I have been working with a customer to help them move a complex Power Apps Canvas app that used a SharePoint Online list backend, to ~~CDS~~ Dataverse. 

This app also has a dependency on using the Power Apps Desktop app which helps provide users with offline capabilities similar to running the app on a mobile app, as it does not run in the browser enabling the use of the `SaveData` and `LoadData` formulas to save and load data from the device whilst offline.

During the development I found myself needing to clear the Power Apps Desktop `SaveData` cache numerous times and I found that it is not the easiest of things to do or best documented, unlike the mobile app which give you an option in the menu to that, with the desktop app it requires you to identify the cache location on the device and remove the cache files manually.

Here are the steps you need to take to do that.

- Open the Run window (*Start -> Run or Win + R*)
- Open `%LocalAppData%`
  - This will open `C:\Users\{username}\AppData\Local` in `File Explorer`
- Open `Packages` folder
- Open `MicrosoftMSApps` folder
  - This will have an identifier at the end, e.g. `Microsoft.MSApps_8wekyb3d8bbwe`
- Navigate to `LocalState` > `14` > `UserSavedData` folder
- Delete all the files in the `UserSavedData` folder

Reopen your app and your cache will be clear 🚀
