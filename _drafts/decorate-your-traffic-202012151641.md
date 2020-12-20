# Decorate Your Traffic 202012151641

To ensure and maintain high-availability, some traffic may be throttled. Throttling happens when system health is at stake and one of the criteria used for throttling is traffic decoration, which impacts directly on the prioritization of the traffic. Well-decorated traffic will be prioritized over traffic, which isn't properly decorated.

Traffic is undecorated if there's no AppID/AppTitle and User Agent string in CSOM or REST API call to SharePoint Online.

To decorate requests and prioritise traffic, the User-Agent header in HTTP requests should be set in the following format

`NONISV|CompanyName|AppName/Version`

The setting of the User-Agent header can be set using the SharePoint HTTP action as well as the HTTP action.