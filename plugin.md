## Plugin API (Version 3)

Bug Shooting provides an API to create custom Outputs. The API is written in .NET so you can create Outputs by using C# or VB.NET.

The previous versions of the Output API ([V1](https://bugshooting.manuscript.com/f/page?W26) and [V2](https://bugshooting.manuscript.com/f/page?W34)) are still supported but will be removed in the future.

### Requirements

- Bug Shooting version 2.16.x or higher
- .NET Framework 4.5.2
- Visual Studio (or some other IDE for .NET)
- Idea for an Output :)

### Examples

For code examples see the open source implementation of various Outputs on [https://github.com/BugShooting](https://github.com/BugShooting).

### Installation

#### Deploy a NuGet Package

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

#### Manual installation

You can also install the Output files manually into Bug Shooting installation.

1. Navigate to the **Custom Output** directory of Bug Shooting installation (usually **%ProgramData%\Bug Shooting 2\Outputs**).
2. Create a sub directory inside **Custom Output** directory using name of your choise. (e.g. the name of the plugin).
3. Copy your Output assembly and all necessary files to this new directory (do not deploy file **BS.Plugin.V3.dll**).
4. Restart Bug Shooting application.
