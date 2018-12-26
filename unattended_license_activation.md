# Unattended license activation

Bug Shooting application also supports an unattended activation of the license. This is usefull for application deployment in conjunction with a volume license.

Create a file **License_Information.xml** inside directoriy **%ProgramData%\Bug Shooting 2** with following content. Replace **???** with your license informations you get during the purchase process.

On application startup the license informations from License_Information.xml will be used for an unattended activation.

## Content of License_Information.xml
```xml
<?xml version="1.0" encoding="utf-16"?>
<BugShootingLicense>
	<RegName>???</RegName>
	<SerialID>???</SerialID>
</BugShootingLicense>
```
