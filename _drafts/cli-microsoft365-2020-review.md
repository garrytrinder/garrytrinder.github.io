# CLI for Microsoft 365 - 2020 in Review

As 2020 concludes and 2021 begins, the CLI for Microsoft 365 enters its fourth year. 

We look back at our highlights and major milestones in 2020. 

## Office 365 CLI is dead, long live CLI for Microsoft 365!

One of the big changes of 2020 was that the CLI underwent a rename to align with Microsoft re-branding of Office 365 to Microsoft 365. 

Why CLI for Microsoft 365 and not Microsoft 365 CLI? As the CLI for Microsoft 365 is a community led project and not an official Microsoft tool we wanted the name to reflect that and standalone.

Whilst changing the name from Office 365 CLI to CLI for Microsoft 365,sounds trivial, it was a major effort to ensure that we removed all traces of Office 365 from the source and our documentation.

We released CLI for Microsoft 365 v3 (previously Office 365 v2) as a major version on 4th September 2020, publishing the new version with a new package name to npm as `@pnp/cli-microsoft365`.

## Increasing the maintainers team

As we started 2020, the CLI had three maintainers, Waldek Mastykarz, Velin Georgiev and Garry Trinder. 

At the beginning of the year, one of the keys goals for 2020 that was discussed was to increase the maintainers team, ensuring that as usage of the CLI grew that we would have the capacity to scale and also help such as issue management, pull request reviews, advocacy and marketing.

By the end of 2020, the maintainers team has grown from three to seven as we welcomed Albert-Jan Schot, Rabia Williams, Patrick Lamber and Mark Powney to the team.

## GitHub Discussions

In April, the CLI for Microsoft 365 GitHub repository was invited to take part in the early beta of GitHub Discussions, previously we used the Gitter platform up to this point, to provide an area for users of the CLI to ask questions and get help from the community, whilst this was a good we felt that it was too isolated from the main GitHub repository and so Discussions appealed in that regard.

It has been great to see a number of features that have been added the CLI directly as a result of members of the community raising Discussions, notably Azure Cloud Shell, Azure Managed Identity support and public Docker images.

## Azure Cloud Shell & Azure Managed Identity support

In May, we were contacted by the Azure Cloud Shell team via GitHub Discussions to look into the possibility of including the CLI in Azure Cloud Shell.

Azure Cloud Shell is an interactive, authenticated, browser-accessible shell for managing Azure resources. It provides the flexibility of choosing the shell experience that best suits the way you work, either Bash or PowerShell.

Working with the team we were able to update our authentication to support Azure Managed Identity removing the need for users to login in to the CLI after logging into the Azure Cloud Shell.

In June, Office 365 CLI v2 was added to the base Azure Cloud Shell image with regular monthly updates and being updated to use CLI for Microsoft 365 CLI in September.

## Sample Scripts

When new commands are added to the CLI we provide usage examples in our documentation, however we understand that in most cases our commands are combined to create scripts.

We started the Sample Scripts repository, a place where bash and PowerShell scripts can be contributed to and stored as working examples alongside the CLI documentation.

At the end of 2020, the community had contributed 27 sample scripts.

## Run CLI for Microsoft 365 in Docker Container

In August, we received feedback via a GitHub Discussion about the possibility of providing public Docker images that could be used to run the CLI in, this was an interesting concept and so we took up the challenges.

In December, we announced the publishing of CLI for Microsoft 365 Docker images to Docker Hub. The images come pre-loaded with all dependencies need to run the CLI, bash and PowerShell, as well as command completion automatically configured for your convenience in both shells.

Every time we publish a new beta or stable version we also release a new version of the Docker image to Docker Hub for you to use immediately after release as part of our CI/CD release pipeline.

## Markshell

With every new command that is added to the CLI, we ensure that there is documentation to accompany the command. As we display help documentation in two places via our web site and interactively at the command line via the `--help` option, this led to maintaining documentation in two places which was a necessary overhead.

In ???, we worked with [Stefan Bauer](https://github.com/StfBauer) the creator of [Markshell](https://github.com/stfbauer/markshell), an npm package that lets you output any Markdown file to the console, to integrate this into the CLI enabling us to consolidate our documentation by rendering the markdown files used on our website directly to the command prompt.

## Removal of Vorpal & request

The Office 365 CLI had two major dependencies, `vorpal`, which is a framework for building a command line interface in nodejs, and `request`, a package that helps simplify making HTTP requests in nodejs. Unfortunately, both these packages were no longer actively maintained and so keeping them posed a risk to the maintainability of the CLI.

Following the release of CLI for Microsoft v3 in September, we removed both dependencies from the CLI, opting to replace the `vorpal` framework with our own code and replacing `request` with `Axios`, a modern alternative to `request`.

## SPFx Doctor

One of the common complaints we hear from SharePoint Developers is knowing whether their development environments are configured correctly for specific versions of SharePoint Framework. 

We created the SPFx Doctor to help solve that problem, running the `spfx doctor` command it will look at dependencies such as Node.js, npm, Yeoman, Gulp, React and TypeScript to verify if they meet the requirements for a particular version of the SharePoint Framework.

## SPFx Project Rename

Naming things is hard, chaning project names after it has been created is even harder.

We created the `spfx project rename` command to enable you to easily rename a SharePoint Framework project without having to manually change the files yourself.

## SPFx Project Upgrades

Two new versions of the SharePoint Framework were released in 2020 and we added support for upgrading your existing projects to the new version days after release.

In January, we added upgrade support for v1.10, and in July we added upgrade support for v1.11 which is currently the latest version of the SharePoint Framework,

Previously, the `spfx project upgrade` command only supported returning the upgrade instructions in markdown.

In May, we released support for generating upgrade instructions as a Code Tour. CodeTour is a Visual Studio Code extension, which allows you to record and playback guided walkthroughs of your codebases, we saw this as a great way to make following the upgrade steps visually in Visual Studio Code, stepping through the changes required directly in the codebase.

## Removal of dev branch and adhoc beta releases

At the beginning of 2020, our approach to new releases was to review PRs at the weekend, if some PRs were reviewed during the week, they'd sit waiting for the upcoming release next weekend. While this pattern gave us a predictable release cadence, often, we'd run of out time reviewing all PRs that the community had contributed and regularly we'd have to let PRs wait for another week or two to review them.

We didn't think that it was fair to let contributors wait for our review longer than was necessary.

To address this, we made two significant changes, the first, we decided that we would release new beta versions as soon as PRs were merged, this meant that PRs reviewed during the week would be immediately released and published to `npm`. The second was to remove the `dev` branch and accept PRs to the `master` branch, enabling us to release beta versions from the master branch, which had previously been released on changes to the `dev` branch.

This change enabled us to increase the frequency of our beta releases, provide faster processing of PRs, increasing the number of new commands, enhancements and bug fixes, whilst keeping the regular cadence of monthly stable releases at the end of each month.

## Year In Numbers

- 460 Commits
- 132842 Downloads 
  - 11228 (v3)
  - 121614 (v2)
- 7,027,970 command executions
- 73 new commands
- 141 beta releases
- 16 stable releases
- [@climicrosoft365] 1,017 followers
- 56 All-time contributor count
- 35 2020 contributor count
 - 14 MVPs
 - 5 MSFT

## Contributors

We would like to extend our thanks to all the community members that have contributed to the CLI in 2020, we appreciate you spending your time to help grow and advance our mission to be the one CLI for managing your SharePoint Framework solutions and your Microsoft 365 tenant. 

Our thanks go to (in alphabetical order):

 - [Albany, Bruce](https://github.com/balbany)
 - [Bernier, Hugo](https://github.com/hugoabernier)
 - [Bhardwaj, Aakash](https://github.com/aakashbhardwaj619)
 - [Biret, Vincent](https://github.com/baywet)
 - [Ford, Lee](https://github.com/leeford)
 - [Georgiev, Velin](https://github.com/VelinGeorgiev) (Maintainer)
 - [Ghuge, Pramod](https://github.com/pramodghuge)
 - [Harding, Phil](https://github.com/phillipharding)
 - [Högberg, Joakim](https://github.com/joakimhogberg)
 - [Kasireddy, Prasad](https://github.com/Prasad_kasiredd)
 - [Khalil, Bassem](https://github.com/BassemNKhalil)
 - [Kumar, Shantha](https://github.com/ktskumar)
 - [Lamber, Patrick](https://github.com/plamber) (Maintainer)
 - [Levert, Sebastien](https://github.com/sebastienlevert)
 - [Maillot, Michaël](https://github.com/michaelmaillot)
 - [Mastykarz, Waldek](https://github.com/waldekmastykarz) (Maintainer)
 - [Menon, Arjun](https://github.com/arjunumenon)
 - [Moujahid, Abderahman](https://github.com/Abderahman88)
 - [Mücklisch, Steve](https://github.com/muecs)
 - [Nachan, Nanddeep](https://github.com/nanddeepn)
 - [Nachan, Smita](https://github.com/SmitaNachan)
 - [Nikolić, Aleksandar](https://github.com/alexandair)
 - [Powney, Mark](https://github.com/mpowney) (Maintainer)
 - [Ramalho, David](https://github.com/DRamalho92)
 - [Rozinov, Roman](https://github.com/romanatsogeti)
 - [Schaeflein, Paul](https://github.com/pschaeflein)
 - [Schot, Albert-Jan](https://github.com/appieschot) (Maintainer)
 - [Shah, Dipen](https://github.com/dips365)
 - [Skelly, Pete](https://github.com/pkskelly)
 - [Struyf, Elio](https://github.com/estruyf)
 - [Tatti, Anoop](https://github.com/anoopt)
 - [Trinder, Garry](https://github.com/garrytrinder/) (Maintainer)
 - [Vaghasia, Siddharth](https://github.com/siddharth-vaghasia)
 - [Velliah, Joseph](https://github.com/sprider)
 - [Williams, Rabia](https://github.com/rabwill) (Maintainer)

We hope that you have enjoyed contributing to the CLI in 2020 and we can't wait to see what we can achieve together in 2021! 

#SharingIsCaring