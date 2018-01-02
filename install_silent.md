<a href="{{ site.url }}">Docs home</a>

# Silent Installation

Bug Shooting installer supports silent installation and uninstallation.

## Available Switches

**/?, /HELP** | Shows available command line switches.
**/SILENT** | Run a silent installation
**/INSTALLPATH** | Path to the install location. Optional.
**/LINKDESKTOP** | Create a link to the desktop. 1=create link, 0=no link. Optional.
**/LINKAUTOSTART** | Create a link to the "startup" Directory. 1=create link, 0=no link. Optional
**/MULTIUSER** | Multi user installation (e.g. for use with Remote Desktop Services). 1=yes, 0=no. Optional
 
## Example

*BugShooting_Setup.exe /SILENT /INSTALLPATH="C:\Program Files\Bug Shooting 2" /LINKDESKTOP=1*
