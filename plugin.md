# Plugin API - Version 3

* [Introduction](#introduction)
* [Requirements](#requirements)
* [Examples](#examples)
* [Reference](#reference)
* [Debug Plugin Code](#debug)
* [Deploy a NuGet Package](#deploynuget)
* [Manual installation](#manualinstallation)

## <a name="introduction"></a>Introduction

Bug Shooting provides a Plugin API to create custom Outputs. The API is written in .NET so you can create Outputs by using C# or VB.NET.

For using the Plugin API add a reference to **BS.Plugin.V3.dll** from Nuget package [BugShooting.Plugin.V3](https://www.nuget.org/packages/BugShooting.Plugin.V3).

> The previous versions of the Output API ([V1](https://bugshooting.manuscript.com/f/page?W26) and [V2](https://bugshooting.manuscript.com/f/page?W34)) are still supported but will be removed in the future.

## <a name="requirements"></a>Requirements

- Bug Shooting version 2.16.x or higher
- .NET Framework 4.5.2
- Visual Studio (or some other IDE for .NET)
- Idea for an Output :)

## <a name="examples"></a>Examples

For code examples see the open source implementation of various Outputs on [https://github.com/BugShooting](https://github.com/BugShooting).

## <a name="reference"></a>Reference

```csharp
namespace BS.Plugin.V3.Common
{

  // Provides the image data which is send to an Output.
  class ImageData
  {
  
    // List of images.
    List<Image> Images { get }
    
    // A merged image of all images from the Images-List.
    Image MergedImage { get }
    
    // Title of the image.
    string Title { get }
    
    // Note of the image.
    string Note { get }
    
    // Create date of the image.
    DateTime CreateDate { get }
    
    // Last change date of the image.
    DateTime ChangeDate { get }
    
  }
  
}

namespace BS.Plugin.V3.Output
{

  // Provides an interface for an Output entity.
  interface IOutput
  {
  
    // Name of the Output entity.
    string Name { get }
    
    // Additional information of the Output entity.
    string Information { get }

  }

  // Provides a generic base class for an Output Plugin.
  // This class provides methods for managing the IOutput.
  class OutputPlugin<IOutput>
  {
  
    // Name of the Output Plugin.
    string Name { get }
    
    // Description of the Output Plugin.
    string Description { get }
    
    // Symbol of the Output Plugin (Size 64 x 64 pixels).
    Image Image64 { get }
    
    // Symbol of the Output Plugin (Size 16 x 16 pixels)
    Image Image16 { get }
    
    // Get the value indicating whether the Output is editable by the user.
    bool Editable { get }

    // Creates a new Output. This method is called if the user add an Output.
    // This method can contains code for opening a form where the properties
    // of the Output can be entered. 
    // If you want to cancel the creation just return null.
    IOutput CreateOutput(IWin32Window Owner)
    
    // Edit an existin Output. 
    // This method can contains code for opening a form where the values
    // of the Output can be changed. 
    // If you want to cancel the editing just return null.
    IOutput EditOutput(IWin32Window Owner, IOutput Output)
    
    // Serialize the Output.
    OutputValues SerializeOutput(IOutput Output)
    
    // Deserialize and return an instance of an Output.
    IOutput DeserializeOutput(OutputValues OutputValues)
    
    // Send an image to an Output.
    SendResult Send(IWin32Window Owner, IOutput Output, ImageData ImageData)
    
  }
  
}

namespace BS.Plugin.V3.Utilities
{

  // Provides helper methods for file operations.
  class FileHelper
  {
  
    // Get the file bytes of an image.
    byte[] GetFileBytes(string FileFormat, ImageData ImageData)
    
    // Get the file extention of a file format.
    string GetFileExtention(string FileFormat)
    
    // Get supported file formats.
    List<string> GetFileFormats()
    
    // Get the mime type of a file format.
    string GetMimeType(string FileFormat)
   
  }
  
  // Provides helper methods for attribute replacements.
  class AttributeHelper
  {
    // Get available attribute replacements.
    IEnumerable<string> GetAttributeReplacements()

    // Replace attributes in the text and returns the result.
    string ReplaceAttributes(string Text, ImageData ImageData)
    
    // Replace attributes in the text and returns the result.
    // This method does not increase values of counter attributes.
    string ReplaceAttributesPreview(string Text, ImageData ImageData)
  }
  
  // Provides helper methods for web operations.
  public class WebHelper
  {
  
    // Open an url in the default browser.
    void OpenUrl(string Url)
    
  }
  
}
```

## <a name="debug"></a>Debug Plugin Code

If is simpel to debug your Plugin code using Visual Studio.

1. Install Bug Shooting on your developer machine.
2. Create a sub directory inside the Bug Shooting **Outputs** directory using name of your choise (example **%ProgramData%\Bug Shooting 2\Outputs\MyOutput**).
3. Set the output derectory of your Plugin project to the previously created directory.
4. Select "**Start external program**" as start action for your Plugin project and set the value to Bug Shooting executable (located here **%ProgramFiles%\Bug Shooting 2\BugShooting2.exe**)
7. Start debugging of your Plugin project.

XXXXXXXXXXXXXXXXXXXX

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

1. Navigate to the **Outputs** directory of your Bug Shooting installation (**%ProgramData%\Bug Shooting 2\Outputs**).
2. Create a sub directory inside the **Outputs** directory using name of your choise (example **%ProgramData%\Bug Shooting 2\Outputs\MyOutput**).
3. Copy your Output assembly and all necessary files to this new directory (do not deploy file **BS.Plugin.V3.dll**).
4. Restart Bug Shooting application.
