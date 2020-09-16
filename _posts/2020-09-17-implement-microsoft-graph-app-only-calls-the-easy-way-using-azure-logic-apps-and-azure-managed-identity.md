---
layout:         post
title:          Implement Microsoft Graph app-only calls the easy way using Azure Logic Apps and Azure Managed Identity
category:       Azure Managed Identity
tags:           [Azure, Logic Apps, Managed Identity, CLI for Microsoft 365, Microsoft Graph]
permalink:      /:year/:month/:title
published:      true
---

This post will show you how you can configure an Azure Logic App to make app only calls to the Microsoft Graph without the need to handle any client credentials such as client ids, secrets or certificates, by using Azure Managed Identity authentication.

By enabling Azure Managed Identities on Azure resources, we can use these identities to authenticate to any service that supports Azure Active Directory authentication.

As Azure manages the identity for us, we gain a number of benefits

- No client credentials to handle
- Automatic credential rolling
- Identies are tied to Azure Resources
- No additional cost

To keep things super simple, our Azure Logic App will just make a single call to return all Microsoft 365 groups in a given tenant using Azure Managed Identity to authenticate with the Microsoft Graph.
 
## Provision the Azure Logic App

- Navigate to the Azure Portal
- Click `Create a resource` 
- Search for `Logic App` and hit return
- Click `Create` on the Logic App screen
- Create a new resource group e.g. `rg-apponly-graph-dev`
- Select an appropriate region e.g. `UK South`
- Enter name for the logic app e.g. `la-apponly-graph-dev`
- Click `Review + Create`
- Click `Create` to provision the Azure Logic App

![](/public/img/managedidentity/create-logic-app.gif){: .center-image }

## Enable Azure Managed Identity on the Azure Logic App

- Open the Logic App after it has been provisioned and scroll to the menu on the left
- Click on the `Identity` menu item under the `Settings` section
- Change the `Status` toggle to `On`
- Click `Save`
- Click `Yes` to the prompt which consents that you understand that an identity will be created in Azure Active Directory

![](/public/img/managedidentity/enable-managed-identity.gif){: .center-image }

> Learn more about Managed Identity on [docs.microsoft.com](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)

## View Azure Managed Identity Service Principal

- Open `Azure Active Directory`
- Click on the `Enterprise Applications` menu item
- Change the `Application type` dropdown to `All`
- Search for the name of the Logic App e.g. `la-apponly-graph-dev`
- Click on the name of the application listed in the table to view the Service Principal details
- Click the `Permissions` menu item under the `Security` section

![](/public/img/managedidentity/view-managed-identity-service-principal.gif){: .center-image }

## Grant the Azure Managed Identity Service Principal Microsoft Graph app only permissions

- Open the `Azure Cloud Shell` from the Azure Portal suite bar (Accept the prompt to create a storage account if you have never used the Cloud Shell before)
- Wait for the Cloud Shell session to start
- Execute `m365 login --authType identity` to login to your Microsoft 365 tenant using Managed Identity authentication
- Execute `m365 status` to confirm login status
- Execute `m365 aad approleassignment add --displayName "la-apponly—graph-dev" --resource "Microsoft Graph" --scope "Group.Read.All"` to grant the Managed Identity Service Prinicpal the Group.Read.All application permission to the Microsoft Graph
- Close the `Cloud Shell` prompt
- Click `Refresh` to update the Permissions and confirm that the new permission has been granted 

![](/public/img/managedidentity/grant-microsoft-graph-permission.gif){: .center-image }

> The tool used in this step is the `CLI for Microsoft 365` which is pre-installed in the Azure Cloud Shell, as it is a cross platform tool it can be used in either `bash` or `PowerShell`. To learn more about the CLI and its features/commands, check out the project [documentation](https://aka.ms/cli-m365)

## Configure the Azure Logic App

- Open the Logic App
- Scroll down to view the `Templates` section and click `Blank Logic App` to open the Logic App Designer
- Search for `Reccurence`, click on `Schedule` and then `Recurrence` to add the trigger action
- Leave the trigger action inputs as the default values
- Click `New step`
- Search for `HTTP`, click on `HTTP` to add the action
- Select `GET` from the dropdown in the `Method` field
- Enter `https://graph.microsoft.com/v1.0/groups` in the `URI` field
- Click on the `Add new parameter` field 
- Check the `Authentication` checkbox
- Click on the design surface (away from the Add new parameter field) to render the `Authentication` section
- Change the `Authentication type` to `Managed Identity`
- Enter `https://graph.microsoft.com` in the `Audience` field
- Click `Save`

![](/public/img/managedidentity/configure-logic-app.gif){: .center-image }

## Manually run the Azure Logic App

- Click the `Run` button in the Logic App Designer to manully trigger the Logic App
- After a few moments the Logic App Designer will display the results of the run
- Click the HTTP action to view the succesful request result

![](/public/img/managedidentity/run-logic-app.gif){: .center-image }

Congratulations! You just pulled data from the Microsoft Graph without having to pass any credentials! 🎉 🚀

## Cleanup

- Open the `Resource Groups` view 
- Click on the resource group e.g. `rg-apponly-graph-dev`
- Click `Delete resource group`
- Enter the name of the resource group in the field e.g. `rg-apponly-graph-dev`
- Click `Delete`
  
> As the Azure Managed Identity Service Principal lifecycle is tied to the resource that created it, it is automatically removed from Azure Active Directory when the resource is deleted

## Summary

Azure Logic Apps and Azure Managed Identity provide a very powerful and highly secure, no-code approach that is ideal for automation scenarios that are incredibly easy to configure.

When working with cloud solutions we should always be ensuring that client credentials and secrets are secured, Azure Managed Identity helps reduce the burden of maintaining and rolling credentials, helping you increase your security in a simple and effective way.

If you would like to learn about how you can use Azure Managed Identity with other Azure Resources such as Azure VMs and Azure Functions, checkout my session recording of `Keyless Authentication using Azure Managed Identity` from the [PnP Virtual Conference](https://pnp.github.io/) held on 1st September 2020.

<div style="text-align:center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/5Ln6xJ6F7vI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
