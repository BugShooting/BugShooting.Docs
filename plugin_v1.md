# Output API - Version 1

> This version will be removed in the future.

## Introduction
Bug Shooting provides an API to create custom Outputs. You can use the API to create your own Outputs which are not supported by Bug Shooting yet. The API is written in .NET 2.0 so you can create Outputs by using C# or VB.NET. 

## Requirements
* Visual Studio 2005 / 2008 / 2010
* Idea for an Output 

## API reference
For using Output API add a reference to **BS.Output.dll** to your .NET project. You will find this assembly in the installation directory of Bug Shooting. You need also references to **System.Drawing** and **System.Windows.Forms**.

### IOutput
Provides an interface for an Output entity.

**Name**
Provides the name of the Output

**Information**
Provides a text which contain a summary of the Output properties.

**OutputAddIn**
Provides a generic base class for an Output addin. This class provide methods for managing the IOutput

**ID**
Provides the unique ID of the addin. This ID is used for internal identification of the addin class. Please use always a new unique ID (Guid) if develop a new addin. You can use the Guid-Generator which is included in the Visual Studio.

**Name**
Provides the name of the Output addin.

**Category**
Provides the category of the Output (BugTracker, InstantMessaging, MediaSharing, Applications or Misc). The category is used to group the output addins.

**Image64x32**
Provides the logo of the Output. The resolution of the image should be width = 64 pixel and height = 32 pixel.

**Image16x16**
Provides a small logo of the Output. The resolution of the image should be width = 16 pixel and height = 16 pixel.

**Editable**
Get the value indicating whether the Output is editable by the user. If an Output is editable the edit button in the settings dialog is enabled when the Output is selected. If the edit button is pressed the EditOutput method is called.

**MultiInstancePossible**
Get the value indicating whether multiple instances of the Output can be added. If the value is False you can add only one instance of this Output type to the Output list.

**CreateOutput**
Creates a new Output. This method is called if the user add an Output in the settings dialog. This method can contain code for opening a form where the properties of the Output can be entered.

**EditOutput**
Edit an exist Output. This method is called if the user edit an exist Output in the settings dialog. This method can contain code for opening a form where the properties of the Output can be changed.

**SerializeOutput**
Convert an Output to an OutputValueCollection which is used to store the Output values in a file.

**DeserializeOutput**
Opposite of SerializeOutput. Create and return an instance of an Output from an OutputValueCollection.

**GetSendOptions**
Get the values which are necessary to send an image to the Output. This method is called after the user clicked on "send to output" button but before the image is sent to the Output. This method can contain code for opening a form where options for sending can be entered (e.g. a description for the image). This method return an instance of IOutputSendOptions or Nothing if no send options necessary. The returned instance of IOutputSendOptions will be passed to the SendImageAsync-Method.

**SendImageAsync**
Send an image to an Output. This method is called after the call of the GetSendOptions-Method and contains code for perform the sending operations.

### SendResult
An instance of this classis passed to the SendImageAsync method and is used to handle the result of the sending operation.

**Result**
State of the sending result. Possible values are Success, Failed and Canceled. This property must be set during the execution of the SendImageAsync method.
 
**ResultMessage**
Text message which will shown to the user if the Result not Success.

**UpdateOutupt**
This property can be used if the vlues of the Output which is passed to the SendImageAsync method must be updated after the send operation. E.g. if you entered login credentials during the sending operation and you want remember the user name an the password for further sending operations, you can set an new instance of your Output (which include the ne values) to the UpdateOutput property. After te SendImageAsync method is finished this new Output instance will be stored in the Output settings.

### OutputValue
Provides a key value pair class which keep a value for serialization and deserialization of an Output.

### OutputValueCollection
Provides a collection of OutputValue.

### IOutputSendOptions
Provides an interface for send options of an Output.

## Install custom Output
1. Navigate to the Custom Output directory of Bug Shooting (location see below).
2. Create a sub directory in the Custom Output directory. Use any name for the directory (e.g. the name of the AddIn).
3. Copy your Output assembly to this new directory.
4. Restart Bug Shooting.

> The location of the Custom Output directory depends on your operating system.
> Windows XP - %AllUsersProfile%\Application Data\Bug Shooting 2\Outputs
> Windows 7 / Vista - %ProgramData%\Bug Shooting 2\Outputs
