This page provides a reference for the LibMan CLI (Library Manager Command Line Interface).

# Commands

The following verbs are available on the LibMan tool:

Options:
- --help|-h
- --version

Commands:
- init
- install
- uninstall
- restore
- clean
- update
- cache

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
- libraryId  Library to install

Options:
<table>
<tr><td>  --help|-h</td><td>Show help information</td></tr>
<tr><td>  --verbosity</td><td>Set the verbosity of output (eg. "normal", "detailed", "quiet")</td></tr>
<tr><td>  --provider|-p</td><td>Provider to use (if not specified, the default provider will be used)</td></tr>
<tr><td>  --destination|-d</td><td>Location to install the library (if not specified, the default destination location will be used)</td></tr>
<tr><td>  --files</td><td>The files from the specified library to install (if not specified, all files from the library will be installed)</td></tr>
</table>

Remarks:<br>
Initializes a libman.json if one does not exist.<br>
If no default provider exists, --provider option is required.<br>
If no default destination exists, --destination option is required.<br>
If no files are specified, the entire library is included.<br>

Examples:
- libman install jquery@3.2.1
- libman install jquery --provider cdnjs --destination wwwroot\scripts\jquery --files jquery.min.js
- libman install myCalendar --provider filesystem --files calendar.js --files calendar.css

