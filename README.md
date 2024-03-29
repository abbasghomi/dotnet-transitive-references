# .Net Transitive Dependencies

*(Transitive references)*



A sample solution to demonstrate how neat can be our projects in referencing, if we use .Net core 1.1 or higher.

This is possible in lower versions with adding a proper tag to csproj files



One of amazing feature introduced in .Net core 1.1 is that you can have transitive dependencies and have access to all public methods and properties in low level  referenced ones  just by referencing the high level one



We have a solution with this structure

![Architecture view](https://github.com/abbasghomi/dotnet-transitive-references/blob/20e7b45288e62750a7527d1467c9a75c7742ee4a/docs/Architecture%20view%20for%20CSharpStandardLibraryAmusements.png)



and now you can use LibraryFive functionalities in the ConsoleApp by just adding reference to LibraryOne in it



![solution_overview](https://github.com/abbasghomi/dotnet-transitive-references/blob/5d0919bf65fb20a48e2bf1e5bec82c54243bf5cf/docs/solution_overview.png)



Another trick: you can break this chain of references by editing a Project file in a text editor and add PrivateAssets="All"  at the end of desired ProjectReference tags

e.g. you can edit LibraryFour.csproj file and change it from

```xml
<Project Sdk="Microsoft.NET.Sdk">
 
  <PropertyGroup>
    <TargetFramework>netstandard2.1</TargetFramework>
  </PropertyGroup>
 
  <ItemGroup>
    <ProjectReference Include="..\LibraryFive\LibraryFive.csproj" />
  </ItemGroup>
 
</Project>
```

to this

```xml
<Project Sdk="Microsoft.NET.Sdk">
 
  <PropertyGroup>
    <TargetFramework>netstandard2.1</TargetFramework>
  </PropertyGroup>
 
  <ItemGroup>
    <ProjectReference Include="..\LibraryFive\LibraryFive.csproj" PrivateAssets="All" />
  </ItemGroup>
 
</Project>
```

And now We have access to LibraryFive project only in LibraryFour project not in any other high level libraries that are referencing LibraryFour.

