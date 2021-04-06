# Upgrade your SharePoint Framework projects the easy way using CLI for Microsoft 365 & Docker

The SharePoint Framework (SPFx) is a page and web part model that provides full support for client-side SharePoint development, easy integration with SharePoint data, and extending Microsoft Teams.

Since it was first released in February 2017, there have been many releases of the framework adding new extensibility capabilities as SharePoint Online and Microsoft Teams have evolved, however upgrading existing projects to new versions of the framework is not a trivial process.

This is where the CLI for Microsoft 365 comes in handy. 

The `spfx project upgrade` command will scan your project and provide a detailed report of required and optional changes that are needed to be made to your project to upgrade it to the latest version.



```sh
docker run --rm -it -v ${PWD}:/home/cli-microsoft365/code -w /home/cli-microsoft365/code m365pnp/cli-microsoft365:latest pwsh -c "m365 spfx project upgrade --shell powershell --output md > report.md"
```

