This page provides a reference for the LibMan CLI (Library Manager Command Line Interface).

# LibMan Commands

Usage: libman [options] [command]

Options:
<table>
<tr><td width="200px">--help|-h</td><td>Show help information</td></tr>
<tr><td>--version</td><td>Show version information</td></tr>
</table>

The following commands are available on the LibMan tool:

Commands:
<table>
<tr><td><a href="#Init">init</a></td><td>Create a new libman.json</td></tr>
<tr><td>install</td><td>Add a library definition to the LibMan.json file, and download the library to the specified location</td></tr>
<tr><td>uninstall</td><td>Deletes all files for the specified library from their specified destination, then removess the specified library definition from libman.json</td></tr>
<tr><td>restore</td><td>Downloads all files from provider and saves them to specified destination</td></tr>
<tr><td>update</td><td>Updates the specified library</td></tr>
<tr><td>clean</td><td>Deletes all library files defined in libman.json from the project</td></tr>
<tr><td>cache</td><td>List or clean libman cache contents</td></tr>
<table>

Use "libman [command] --help" for more information about a command.


# Command Details

## Help flag

Usage: --help|-h

Prints a list of all available LibMan verbs.<br>
If parameter supplied, will print the full details of the supplied verb.

Examples:
- libman --help
- libman -h

## Version flag

Usage: --version

Prints the current version of the LibMan executable.

Examples:
- libman --version

## Init

Usage: libman init [options]

Options:<br>
<table>
<tr><td width="200px">--help|-h</td><td>Show help information</td></tr>
<tr><td>--verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
<tr><td>--default-provider|-p</td><td>The provider to use if no provider is defined for a given library. (eg. “cdnjs”, “filesystem”)</td></tr>
<tr><td>--default-destination|-d</td><td>The path, relative to the current directory, where library files should be installed if no destination is defined for a given library.</td></tr>
</table>

Remarks:<br>
Creates new libman.json in the current directory.<br>
Will throw an error if libman.json already exists.<br>
Will prompt for a defaulDestination if none provided.

Examples:
- libman init  (interactive)
- libman init --default-provider "cdnjs"
- libman init --version "1.0"
- libman init --version 1.0 --default-provider cdnjs --default-destination script\libman

## Install

Usage: libman install [arguments] [options]

Arguments:
<table>
<tr>
<td width="200px">libraryId</td>
<td>Library to uninstall</td>
</tr>
</table>

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
<tr><td>  --provider|-p</td><td>Provider to use (if not specified, the default provider will be used)</td></tr>
<tr><td>  --destination|-d</td><td>Location to install the library (if not specified, the default destination location will be used)</td></tr>
<tr><td>  --files</td><td>The files from the specified library to install (if not specified, all files from the library will be installed)</td></tr>
</table>

Remarks:<br>
Adds the specified library definition to the libman.json and downloads the files to the destination specified.<br>
Initializes a libman.json if one does not exist.<br>
If no default provider exists, --provider option is required.<br>
If no default destination exists, --destination option is required.<br>
If no files are specified, the entire library is included.<br>

Examples:
- libman install jquery@3.2.1
- libman install jquery --provider cdnjs --destination wwwroot\scripts\jquery --files jquery.min.js
- libman install myCalendar --provider filesystem --files calendar.js --files calendar.css

## Uninstall

Usage: libman uninstall [arguments] [options]

Arguments:
<table>
<tr>
<td width="200px">libraryId</td>
<td>Library to uninstall</td>
</tr>
</table>

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
</table>

Remarks:<br>
Deletes the library file/s from the specified destination, then remove the specified library config from libman.json.
Will throw error if no libman.json in current folder<br>
Will throw error if specified library doesn't exist<br>
If there's more than one library with the same libraryId, you'll be prompted to choose.<br>

Examples:
- libman uninstall jquery
- libman uninstall jquery@3.3.1

## Restore

Usage: libman restore [options]

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
</table>

Remarks:<br>
Downloads all files from provider and saves them to configured destination.<br>
Will throw error if no libman.json in current folder<br>
If a library specifies a provider, it will override the defaultProvider<br>
If a library specifies a destination, it will override the defaultDestination<br>

## Update

Usage: libman update [arguments] [options]

Arguments:
<table>
<tr>
<td width="200px">libraryId</td>
<td>Library to update</td>
</tr>
</table>

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
<tr><td>  -pre</td><td>If specified, the latest pre-release version of the library will be downloaded (where applicable)</td></tr>
<tr><td>  --to</td><td>The version to update the library to (needs complete libraryid for the provider)</td></tr>
</table>

Remarks:<br>
Updates the specified library to the latest version.<br>
Error if no libman.json in current folder<br>
Error if specified library doesn't exist<br>
If there's more than one library with the same libraryId, you'll be prompted to choose.<br>

Examples:
-    libman update jquery
-    libman update jquery --to 3.3.1
-    libman update jquery -pre

## Clean

Usage: libman clean [options]

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
</table>

Remarks:<br>
Deletes from the local project all library files defined in libman.json.<br>
Deletes any folders that become empty after this operation.<br>

## Cache

Usage: libman cache [options] [command]

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
</table>

Commands:
<table>
<tr><td>clean</td><td>Delete all files from the local machine's LibMan cache.</td></tr>
<tr><td>list</td><td>Display a list of all libraries that are stored in the local machine’s LibMan cache.</td></tr>
</table>

### Cache Clean

Usage: libman cache clean [arguments] [options]

Arguments:
<table>
<tr>
<td width="200px">provider</td>
<td>Provider for which the cache files should be cleaned.</td>
</tr>
</table>

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
</table>

Remarks:<br>
Delete all files from the local machine's LibMan cache. (This is the local cache that's usually kept in the user's home directory.)

### Cache List

Usage: libman cache list [arguments] [options]

Options:
<table>
<tr><td width="200px">  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
<tr><td>  --files</td><td>List files that are cached for each library.</td></tr>
<tr><td>  --libraries</td><td>List the libraries cached for each provider.</td></tr>
</table>

Remarks:<br>
Lists the libraries in the local machine's LibMan cache. (This is the local cache that's usually kept in the user's home directory.)