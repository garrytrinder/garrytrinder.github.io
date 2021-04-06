# Testing Azure Functions in dotnet with xUnit

Starting directory

- MyFunctionSolution
  - Functions
    - Functions.csproj
    - HttpFunction.cs
  - MyFunctionSolution.sln

```sh
dotnet new xunit --name Functions.Tests
```
New directory

- Functions
  - Functions
    - Functions.csproj
    - HttpFunction.cs
  - Functions.Tests
    - Functions.Tests.csproj
    - UnitTest1.cs
  - MyFunctionSolution.sln

Add new project to solution

```sh
dotnet sln add Functions.Tests
```

Confirm that tests run

```sh
dotnet test
```

Create reference to Functions project

```sh
dotnet add Functions.Tests reference Functions
```
