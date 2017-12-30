# Plugin API - Version 3

Bug Shooting provides an API to create custom Outputs. The API is written in .NET so you can create Outputs by using C# or VB.NET.

The previous versions of the Output API ([V1](https://bugshooting.manuscript.com/f/page?W26) and [V2](https://bugshooting.manuscript.com/f/page?W34)) are still supported but will be removed in the future.

## Requirements

- Bug Shooting version 2.16.x or higher
- .NET Framework 4.5.2
- Visual Studio (or some other IDE for .NET)
- Idea for an Output :)

## Examples

For code examples see the open source implementation of various Outputs on [https://github.com/BugShooting](https://github.com/BugShooting).

## Plugin interfaces

For using the Plugin API add a reference to **BS.Plugin.V3.dll** from Nuget package [BugShooting.Plugin.V3](https://www.nuget.org/packages/BugShooting.Plugin.V3).

### IOutput

Provides an interface for an Output entity.

* IOutput|Provides the name of the Output.
 * IOutput|Provides extended information of the Output.
  * IOutput|Provides extended information of the Output.
  * IOutput|Provides extended information of the Output.
 * IOutput|Provides extended information of the Output.
    

Name|Provides the name of the Output.
Information|Provides extended information of the Output.


BS.Plugin.V3.Utilities.**AttributeHelper**

BS.Plugin.V3.Utilities.**FileHelper**

BS.Plugin.V3.Utilities.**WebHelper**


## Deploy a NuGet Package

After you've developed your awesome Output you can share it with the whole world by deploying a NuGet package to [nuget.org](https://www.nuget.org). See also [existing online packages](https://www.nuget.org/packages?q=Tags%3A%22bugshooting.plugin.v3.output%22).

**What you need to do?**
1. Create a NuGet package including your Output assemblies (do not include file **BS.Plugin.V3.dll**)
2. Include the tag "**bugshooting.plugin.v3.output**" in your package
3. Upload your package to [nuget.org](https://www.nuget.org)
4. Activate the listing of your package on nuget.org

For example package definitions see Output implementations on [https://github.com/BugShooting](https://github.com/BugShooting).

## Manual installation

You can also install the Output files manually into your Bug Shooting installation.

1. Navigate to the **Outputs** directory of your Bug Shooting installation (usually **%ProgramData%\Bug Shooting 2\Outputs**).
2. Create a sub directory inside the **Outputs** directory using name of your choise (exsample **%ProgramData%\Bug Shooting 2\Outputs\MyOutput**).
3. Copy your Output assembly and all necessary files to this new directory (do not deploy file **BS.Plugin.V3.dll**).
4. Restart Bug Shooting application.
