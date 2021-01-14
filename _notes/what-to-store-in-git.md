# What should I store in a git repository

In the previous we talked about version control systems, their benefits and the popular git version control system, but what should we store in our repositories? There are three types of files that we should be storing under version control.

Application code 
This should be any file that is used in the development or build of an application, this could be a full dotnet core application written in C# or a simple PowerShell script.

Application documentation
Documentation should be stored as close to the working code as possible and should be updated as an when the code stored in the repository is changed. The documentation is usually written in markdown and can ranges from a simple readme file to a full documentation site like MKDocs which can be published as a website and is very popular in the open source projects.

Small binary sources
Whilst we do not store the compiled versions of application code, we should be storing small binary files, these are files that are infrequently updated and are not plain text. Examples of small binary sources are exported Power App ZIP file, Power BI PBIX file, Microsoft Word document.
