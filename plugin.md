# Plugin API - Version 3

* [Introduction](#introduction)
* [Requirements](#requirements)
* [Examples](#examples)
* [Reference](#reference)
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

  // XXXXXXXXXXXXXXXXXXXXXXX
  class FileHelper
  {
  
    // XXXXXXXXXXXXXXXXXXXXXXX
    byte[] GetFileBytes(string FileFormat, ImageData ImageData)
    
    // XXXXXXXXXXXXXXXXXXXXXXX
    string GetFileExtention(string FileFormat)
    
    // XXXXXXXXXXXXXXXXXXXXXXX
    List<string> GetFileFormats()
    
    // XXXXXXXXXXXXXXXXXXXXXXX
    string GetMimeType(string FileFormat)
   
  }
  
  // XXXXXXXXXXXXXXXXXXXXXXX
  class AttributeHelper
  {
    // XXXXXXXXXXXXXXXXXXXXXXX
    IEnumerable<string> GetAttributeReplacements()

    // XXXXXXXXXXXXXXXXXXXXXXX
    string ReplaceAttributes(string Text, ImageData ImageData)
    
    // XXXXXXXXXXXXXXXXXXXXXXX
    string ReplaceAttributesPreview(string Text, ImageData ImageData)
  }
  
  // XXXXXXXXXXXXXXXXXXXXXXX
  public class WebHelper
  {
  
    // XXXXXXXXXXXXXXXXXXXXXXX
    void OpenUrl(string Url)
    
  }
  
}

```


**ImageData** *(BS.Plugin.V3.Common)*
> Provides the image data which is send to an Output.

* Images** List of images.
    * **MergedImage** A merged image of all images from the Images-List.
    * **Title** Title of the image.
    * **Note** Note of the image.
    * **CreateDate** Create date of the image.
    * **ChangeDate** Change date of the image.


* BS.Plugin.V3.Common
  * **ImageData** Provides the image data which is send to an Output.
    * **Images** List of images.
    * **MergedImage** A merged image of all images from the Images-List.
    * **Title** Title of the image.
    * **Note** Note of the image.
    * **CreateDate** Create date of the image.
    * **ChangeDate** Change date of the image.
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
    * **GetAttributeReplacements** XXXXXXXXXXXXXXXXXXXXXXX
    * **ReplaceAttributes** XXXXXXXXXXXXXXXXXXXXXXX
    * **ReplaceAttributesPreview** XXXXXXXXXXXXXXXXXXXXXXX
  * **FileHelper** XXXXXXXXXXXXXXXX
      * **GetFileFormats** XXXXXXXXXXXXXXXXXXXXXXX
      * **GetFileBytes** XXXXXXXXXXXXXXXXXXXXXXX
      * **GetFileExtention** XXXXXXXXXXXXXXXXXXXXXXX
      * **GetMimeType** XXXXXXXXXXXXXXXXXXXXXXX
  * **WebHelper** XXXXXXXXXXXXXXXXXXXXXXXX
    * **OpenUrl** XXXXXXXXXXXXXXXXXXXXXXX
  
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
2. Create a sub directory inside the **Outputs** directory using name of your choise (example **%ProgramData%\Bug Shooting 2\Outputs\MyOutput**).
3. Copy your Output assembly and all necessary files to this new directory (do not deploy file **BS.Plugin.V3.dll**).
4. Restart Bug Shooting application.
