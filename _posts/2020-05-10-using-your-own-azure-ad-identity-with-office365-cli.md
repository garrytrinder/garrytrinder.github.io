---
layout:         post
title:          Using your own Azure AD identity with Office 365 CLI
category:       Office 365 CLI
tags:           [Office 365 CLI, Azure Active Directory, Azure AD, Device Code Flow, OAuth]
permalink:      /:year/:month/:title
published:      true
---

The Office 365 CLI provides a quick and easy way to manage your Office 365 tenant from any operating system and any shell. 

When you use the Office 365 CLI to connect to your tenant for the first time, you are presented with a `Permissions requested` prompt from Azure, by accepting this prompt you are consenting to using the `PnP Office 365 Management Shell` Azure AD application with your tenant as well as the permissions that it requires.

We ask for a wide range to permissions up front, including permissions that require administrative level consent, so that it is easy for to get started with the CLI and try out the commands across many Office 365 CLI workloads in your tenant without having to handle the complexity of managing the permissions for the different commands manually in Azure.

Whilst this is fine for working against development and test environments, using these levels of permissions against production environments is inconvenient and administrators are not comfortable with granting such permissions to a multi-tenant application within their environment.

In this scenario, administrators will want to provide their own Azure AD app registration to use with the CLI to enable greater control over the permissions that are granted. 

This tutorial will walk you through how to create your own Azure AD application with permissions restricted to only read information about SharePoint Online Site Collections and how to use this custom application with the Office 365 CLI.

## Register Azure AD application in your tenant

We first need to register a new Azure AD application in your tenant, to do this we will need to navigate to the [Azure Portal](https://portal.azure.com).

Select `Azure Active Directory` from the global menu, select `App registrations` in the Azure Active Directory blade and then select the `New registration` action button to open the `Register an application` form.

![](/public/img/o365cli/o365cli-custom-app-registration_18.png){: .center-image }

In the form, enter a name for your new application, for the purposes of this tutorial lets use `Custom PnP Office 365 CLI`, you can always change this later if you want. Leave the `Supported account types` and `Redirect URI` as they are and select the `Register` button at the foot of the form to create your custom application. 

![](/public/img/o365cli/o365cli-custom-app-registration_17.png){: .center-image }

After the application has been created, you will be presented with the blade for your application displaying an overview of some properties of the application. At this point it is a good idea to take note of two key pieces of information that we will need later.

![](/public/img/o365cli/o365cli-custom-app-registration_16.png){: .center-image }

Take a copy of both the `Application (client) ID` and `Directory (tenant) ID` values and save them to a place for you to refer back to them later.

### Confgure Authentication settings

We next need to configure our new application so that it can be used with the Office 365 CLI, to do this we need select `Authentication` in the `Custom PnP Office 365 CLI` blade menu. 

This will present you with three sections, `Platform configuration`, `Supported account type` and `Advanced settings`.

Select the `Add a platform` button to open up the `Configure platforms` menu and select `Mobile and desktop applications` under the `Mobile and desktop applications` heading, this will open another menu called `Configure Desktop + Devices` displaying a section called `Redirect URIs` and a list of checkboxes with some pre-defined URIs.

![](/public/img/o365cli/o365cli-custom-app-registration_14.png){: .center-image }

Select the first option in the list, `https://login.microsoftonline.com/common/oauth2/nativeclient` and select the `Configure` button at the foot of the menu.

![](/public/img/o365cli/o365cli-custom-app-registration_13.png){: .center-image }

This will refresh the `Authentication` blade and will display the Redirect URI we just chose from the menu.

![](/public/img/o365cli/o365cli-custom-app-registration_11.png){: .center-image }

> This Redirect URI is specific to the use of authentication methods that do not use a web interface for authenticating users and are therefore called `Native Clients`, this is the category that the Office 365 falls into.

Moving on, we can skip over the `Supported account type` section, as this is defaulted to `Accounts in this organizational directory only (<tenant> only - Single tenant)` it means that only users within the current tenant directory can use this identity and onto the `Advanced settings` section, in here we need to toggle the `Default client type` toggle so that is enabled, as we are using the `Device code flow` method to authenticate to our tenant using the Office 365 CLI.

![](/public/img/o365cli/o365cli-custom-app-registration_12.png){: .center-image }

To make sure all these changes are applied, select the `Save` button before moving on.

### Configure API Permissions

Now that we have configured the application to work with the Office 365 CLI, we next need to grant what permissions the CLI will have against our tenant. Select the `API permssions` in the `Custom PnP Office 365 CLI` blade menu.

You will see a section called `Configured permissions` with one permission already granted, this is the defaul permission which allows the application to sign the user account used when authenticating to the Microsoft Graph. 

![](/public/img/o365cli/o365cli-custom-app-registration_10.png){: .center-image }

Select the `Add a permission` button to open the `Request API permissions` menu, as we are only interested in granting our application access to SharePoint Online for the purpose of this tutorial, select `SharePoint` in the list of APIs that are available.

![](/public/img/o365cli/o365cli-custom-app-registration_9.png){: .center-image }

This opens the menu with two options `Delegated permissions` or `Application permissions`, as we are going to be communicating with the SharePoint Online APIs as the authenticated user, select `Delegated permissions`, this will display a list of available permissions that we can choose from.

For the purpose of this tutorial we only want to grant read access to SharePoint Online, so expand the `AllSites` grouping and select the `AllSites.Read` permissions and select the `Add permssions` button to apply these permissions.

![](/public/img/o365cli/o365cli-custom-app-registration_8.png){: .center-image }

> Note that the `AllSites.Read` permission does not directly grant the signed-in user access to all sites in SharePoint Online. As we authenticate as the signed-in user, that user must still have access to the SharePoint sites that we want to return information about, otherwise the SharePoint Online API calls will fail with `401 Unathorized`

You will be presented with the `Configured permissions` section again but this time the `AllSites.Read` permission will be shown under the `SharePoint` grouping.

![](/public/img/o365cli/o365cli-custom-app-registration_7.png){: .center-image }

This completes the configuration required in the Azure portal, we can now move onto configuring the Office 365 CLI to use our custom application to login to Office 365.

## Create Office 365 CLI environment variables

To configure the Office 365 CLI to use our newly created custom application, we need to tell it the Client ID of our custom application and the Tenant ID of where the custom application has been created. 

To do that, we need to create two environment variables, called `OFFICE365CLI_AADAPPID` and `OFFICE365CLI_TENANT`, giving them the values that you saved earlier.

How you set the environment variables is dependant on the operating system and shell you are using.

If you are on Windows, you can set the environment variables using the `$env:<variable-name>` approach in a PowerShell session.

```
$env:OFFICE365CLI_AADAPPID="506af689-32aa-46c8-afb5-972ebf9d218a"
$env:OFFICE365CLI_TENANT="e8954f17-a373-4b61-b54d-45c038fe3188"
```

> Execute `$env:OFFICE365CLI_AADAPPID` and `$env:OFFICE365CLI_TENANT` to verify that the environment variables have been created correctly

If you using Linux or MacOS, you can set the environment variables using the `export` command from your terminal prompt.

```
export OFFICE365CLI_AADAPPID=506af689-32aa-46c8-afb5-972ebf9d218a
export OFFICE365CLI_TENANT=e8954f17-a373-4b61-b54d-45c038fe3188
```

> Execute `printenv` to verify that the environment variables have been created correctly

Now that we have set our environment variables, we are now ready to use our custom application to log in with using the Office 365 CLI.

### Login and consent

For the purpose of this tutorial, we will be using the `Device code flow` to interactively authenticate with an Office 365 CLI tenant. As this is the first time that we will have used the custom application to authenticate, we will also be required to give our consent.

At your terminal session, execute `o365 login` to start the authentication process, a login device code will be displayed along with a link to a web page where it needs to be entered. Navigate to [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin), enter the code into the input field and select `Next`. You will then be presented with either a login screen or accounts that you have already logged in to Office 365 with. Login with or choose the account from the list that you want to use with Office 365 CLI.

You will now be prompted to consent that the custom application, `Custom PnP Office 365 CLI`, can use the two permissions that we configure earlier, `Read items in all site collections` and `Sign you in and read your profile` on your behalf. Select `Accept` to consent and complete the sign-in process.

Returning back to your command line, you can now verify that the sign in has been succesful by executing the `o365 status` command. 

Finally, to test that we can indeed read SharePoint Online site collections, lets invoke the following command

```
o365 spo site get --url https://trinder365dev.sharepoint.com -o json --pretty
```

The JSON representation of the SharePoint Online site will be returned to the console.

Congratulations! You have just configured the Office 365 CLI to use your own custom application with custom permissions from your own Azure Active Directory.

![](/public/img/o365cli/o365cli-custom-app-registration_1.png){: .center-image }

### Find out more

If you would like to know more about Office 365 CLI, visit the web site at [https://aka.ms/o365cli](aka.ms/o365cli). 

If you see any room for improvement or suggestions, please don’t hesitate to reach out to us either on [GitHub](https://github.com/pnp/office365-cli/discussions) or [@office365cli](https://twitter.com/office365cli) on Twitter.

### Appendix: Persisting environment variables

As mentioned earlier, the way in which we set the environment variables meant that they are only set for the lifetime of the session, if the terminal session is closed, you will need to repeat those steps, which maybe undesirable.

How you permanently set the environment variable is dependant on the operating system and shell you are using.

If you are on Windows, you can set the environment variables using the `Edit the system environment variables` approach in the Windows UI.

Search for `Edit the system environment variables` in Start Menu and launch it. Select `Environment Variables`, under the `User variables for <user-name>` section, select `New...` to open a dialog. In the dialog, enter `OFFICE365CLI_AADAPPID` in the variable name field and set the value using the Client ID (quotes should be ommitted), select `OK` to save the value and repeat the process for the `OFFICE365CLI_TENANT` variable. Select `OK` until all windows are closed to persist the changes. 

Open a new PowerShell session and execute `$env:OFFICE365CLI_AADAPPID` and `$env:OFFICE365CLI_TENANT` to verify that the environment variables have been created correctly.

If you are on Linux or MacOS, depending on your terminal, add the  `export` lines to `.bashrc` or `.zshrc` file in your home directory.

If you are using PowerShell Core, it is worth noting that environment variables set in `bash` or `zsh` will persist to the `pwsh` session and the same applies to Windows.