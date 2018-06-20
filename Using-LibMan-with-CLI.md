This page provides a reference for the LibMan CLI (Library Manager Command Line Interface).

# Commands

The following verbs are available on the LibMan tool:
- --version|-v
- --help|-h
- init
- install
- uninstall
- restore
- clean
- update
- cache

# Command Details

## Version flag

Syntax: --version|-v

Prints the current version of the LibMan executable.

Examples:
- libman --version
- libman -v

## Help flag

Syntax: --help|-h

Prints a list of all available LibMan verbs.<br>
If parameter supplied, will print the full details of the supplied verb.

Examples:
- libman --help
- libman -h

## Init

Syntax: init [--version|-v version] [--defaultProvider provider] [--defaultDestination destination]

Creates new libman.json in the current directory.<br>
Will throw an error if libman.json already exists.<br>
Will prompt for a defaulDestination if none provided.

Examples:
- libman init  (interactive)
- libman init --provider "cdnjs"
- libman init --version "1.0"
- libman init --version 1.0 --provider cdnjs --defaultDestination script\libman