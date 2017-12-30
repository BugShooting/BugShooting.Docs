# Plugin API - Version 3

* [Introduction](#introduction)
* [Requirements](#requirements)
* [Examples](#examples)
* [Reference](#reference)
* [Deploy a NuGet Package](#deploynuget)
* [Manual installation](#manualinstallation)

## <a name="introduction"></a>Introduction

Bug Shooting provides an API to create custom Outputs. The API is written in .NET so you can create Outputs by using C# or VB.NET.

The previous versions of the Output API ([V1](https://bugshooting.manuscript.com/f/page?W26) and [V2](https://bugshooting.manuscript.com/f/page?W34)) are still supported but will be removed in the future.

For using the Plugin API add a reference to **BS.Plugin.V3.dll** from Nuget package [BugShooting.Plugin.V3](https://www.nuget.org/packages/BugShooting.Plugin.V3).

## <a name="requirements"></a>Requirements

- Bug Shooting version 2.16.x or higher
- .NET Framework 4.5.2
- Visual Studio (or some other IDE for .NET)
- Idea for an Output :)

## <a name="examples"></a>Examples

For code examples see the open source implementation of various Outputs on [https://github.com/BugShooting](https://github.com/BugShooting).

## <a name="reference"></a>Reference

* BS.Plugin.V3.Common
  * **ImageData** XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    * **xxx** sfsfsfsfdsdf456456sfsdf
    * **xfggggggxx** sfsfsfs346 46fdsdfsfsdf
    * **x456xx** sfsf456sfsfdsdfsfsdf
* BS.Plugin.V3.Output 
  * **IOutput** Provides an interface for an Output entity.
    * **Name** Provides the name of the Output.
    * **Information** Provides extended information of the Output.
  * **OutputPlugin \<IOputput\>** Provides a generic base class for an Output Plugin. This class provides methods for managing the IOutput.
    * **Name** Provides the name of the Output Plugin.
    * **Description** Provides the description of the Output Plugin.
    * **Image64** Provides the logo of the Output Plugin (64 x 64 pixels).
    * **Image16** Provides a small logo of the Output Plugin (16 x 16 pixels).
    * **Editable** Get the value indicating whether the Output is editable by the user.
    * **CreateOutput** Creates a new Output. This method is called if the user add an Output. This method can contains code for opening a form where the properties of the Output can be entered. If you want to cancel the creation just return null.
    * **SerializeOutput** Serialize the Output properties.
    * **DeserializeOutput** Deserialize and return an instance of an Output.
    * **Send** Send an image to an Output.
* BS.Plugin.V3.Utilities
  * **AttributeHelper** XXXXXXXXXXXXXXXXXXXXXX
  * **FileHelper** XXXXXXXXXXXXXXXX
  * **WebHelper** XXXXXXXXXXXXXXXXXXXXXXXX
  
## <a name="deploynuget"></a>Deploy a NuGet Package

After you've developed your awesome Output you can share it with the whole world by deploying a NuGet package to [nuget.org](https://www.nuget.org). See also [existing online packages](https://www.nuget.org/packages?q=Tags%3A%22bugshooting.plugin.v3.output%22).

**What you need to do?**
1. Create a NuGet package including your Output assemblies (do not include file **BS.Plugin.V3.dll**)
2. Include the tag "**bugshooting.plugin.v3.output**" in your package
3. Upload your package to [nuget.org](https://www.nuget.org)
4. Activate the listing of your package on nuget.org

For example package definitions see Output implementations on [https://github.com/BugShooting](https://github.com/BugShooting).

## <a name="manualinstallation"></a>Manual installation

You can also install the Output files manually into your Bug Shooting installation.

1. Navigate to the **Outputs** directory of your Bug Shooting installation (usually **%ProgramData%\Bug Shooting 2\Outputs**).
2. Create a sub directory inside the **Outputs** directory using name of your choise (exsample **%ProgramData%\Bug Shooting 2\Outputs\MyOutput**).
3. Copy your Output assembly and all necessary files to this new directory (do not deploy file **BS.Plugin.V3.dll**).
4. Restart Bug Shooting application.
