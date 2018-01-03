# Output API - Version 2

> This version will be removed in the future.

## Introduction
Bug Shooting provides an API to create custom Outputs. The API is written in .NET so you can create Outputs by using C# or VB.NET. For using the API Bug Shooting 2.10.x or higher is required.

* Bug Shooting 2.10.x requires .NET Framework 3.5
* Bug Shooting 2.14.x requires .NET Framework 4.5.2

## Requirements
* Visual Studio (or some other IDE for .NET)
* Idea for an Output 

## API Reference
For using Output API add a reference to **BS.Output.dll** to your .NET project. You will find this assembly in the installation directory of Bug Shooting. You need also references to **System.Drawing** and **System.Windows.Forms**.

You can also get the reference using NuGet Package. Search for "Bug Shooting Output API" in the NuGet Package Manager or visit NuGet.org.

### IOutput (Interface)
Provides an interface for an Output entity.

> Namespace: BS.Output

**Name**|Provides the name of the Output.
**Information**|Provides a text which contain a summary of the Output properties.

### OutputAddIn (Class)
Provides a generic base class for an Output Add-In. This class provides methods for managing the IOutput.

> Namespace: BS.Output.V2

**ID**|Provides the unique ID of the Add-In. This ID is used for internal identification of the Add-In class. Please use always a new unique ID (Guid) if develop a new Add-In. You can use the Guid-Generator which is included in the Visual Studio.
**Name**|Provides the name of the Output Add-In.
**Description**|Provides the description of the Output Add-In.
**Category**|Provides the category of the Output (BugTracker, InstantMessaging, MediaSharing, Applications or Misc). The category is used to group the Output Add-Ins.
**GroupName**|Privides a group name for an Add-In. You can use this property to group different versions on an Output Add-In.
**Image64x32**|Provides the logo of the Output. The resolution of the image should be width = 64 pixel and height = 32 pixels.
**Image16x16**|Provides a small logo of the Output. The resolution of the image should be width = 16 pixel and height = 16 pixels.
**Editable**|Get the value indicating whether the Output is editable by the user. If an Output is editable the edit button in the settings dialog is enabled when the Output is selected. If the edit button is pressed the EditOutput method is called.
**MultiInstancePossible**|Get the value indicating whether multiple instances of the Output can be added. If the value is False you can add only one instance of this Output type to the Output list.
**CreateOutput**|Creates a new Output. This method is called if the user add an Output in the settings dialog. This method can contain code for opening a form where the properties of the Output can be entered. If you want to cancel the creation just return Null/Nothing.
**EditOutput**|Edit an exist Output. This method is called if the user edit an exist Output in the settings dialog. This method can contain code for opening a form where the properties of the Output can be changed. If you want to cancel the editing just return Null/Nothing.
**SerializeOutput**|Convert an Output to an OutputValueCollection which is used to store the Output values in a file.
**DeserializeOutput**|Opposite of SerializeOutput. Create and return an instance of an Output from an OutputValueCollection.
**GetSendOptions**|Get the values which are necessary to send an image to the Output. This method is called after the user clicked on "send to output" button but before the image is sent to the Output. This method can contain code for opening a form where options for sending can be entered (e.g. a description for the image). This method return an instance of IOutputSendOptions or Nothing if no send options necessary. The returned instance of IOutputSendOptions will be passed to the SendImageAsync-Method.
**SendAsync**|Send an image to an Output. This method is called after the call of the GetSendOptions-Method and contains code for perform the sending operations.
 
### SendResult (Class)
An instance of this classis passed to the SendImageAsync method and is used to handle the result of the sending operation.

> Namespace: BS.Output

**Result**|State of the sending result. Possible values are Success, Failed and Canceled. This property must be set during the execution of the SendImageAsync method.
**ResultMessage**|Text message which will shown to the user if the Result not Success.
**UpdateOutupt**|This property can be used if the vlues of the Output which is passed to the SendAsync method must be updated after the send operation. E.g. if you entered login credentials during the sending operation and you want remember the user name an the password for further sending operations, you can set an new instance of your Output (which include the ne values) to the UpdateOutput property. After te SendAsync method is finished this new Output instance will be stored in the Output settings.
 
### OutputValue (Class)
Provides a key value pair class which keep a value for serialization and deserialization of an Output.

> Namespace: BS.Output

### OutputValueCollection (Class)
Provides a collection of OutputValue.

> Namespace: BS.Output

### IOutputSendOptions (Interface)
Provides an interface for send options of an Output.

> Namespace: BS.Output

## Install custom Output
1. Navigate to the Custom Output directory of Bug Shooting (%ProgramData%\Bug Shooting 2\Outputs).
2. Create a sub directory in the Custom Output directory. Use any name for the directory (e.g. the name of the AddIn).
3. Copy your Output assembly to this new directory.
4. Restart Bug Shooting.
