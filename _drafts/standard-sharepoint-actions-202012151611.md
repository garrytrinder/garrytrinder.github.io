# Standard SharePoint Actions 202012151611

Azure Logic Apps have the ability to use standard SharePoint actions, these actions provide an abstraction layer over the SharePoint API to provide a simplified user interface for common interactions with SharePoint through the SharePoint API.

Whilst there is a potential benefit from a support and maintenance perspective, the actions are limiting for the following reasons

- The API request sent is not fully visible
- Unable to define request headers
- Supports user (delegated) authentication only
- API requests are not fully visible

As these actions abstract away the complexities of making requests to SharePoint, they work like black boxes, so when issues arise it can make it more difficult to diagnose as you do not get the full picture of the request.

These actions are also limited to only using [[delegated-authentication-202012151621]] so there is a requirement for the Logic Apps to use a user identity for making authenticated requests to SharePoint such as a service account, however this approach in high usage scenarios can increase the likelihood of [[throttling-202012151623]].

See [[optimising-logic-apps-costs-202012151720]] for pricing comparisons.

#logicapps #cost

[//begin]: # "Autogenerated link references for markdown compatibility"
[delegated-authentication-202012151621]: delegated-authentication-202012151621 "Delegated Authentication 202012151621"
[//end]: # "Autogenerated link references"