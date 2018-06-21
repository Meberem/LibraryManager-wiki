Here's a handy cheat sheet for getting started with LibMan CLI

## Get the LibMan global tool

Before you can use LibMan from the CLI, you must first download and install the global tool via the dotnet CLI.

`> dotnet tool install -g libman`

If you need to install LibMan from an alternative location, use the following syntax.

`> dotnet tool install -g libman --version 1.0.94-g606058a278 --add-source C:\Temp\`

Will install LibMan CLI from C:\Temp\libman.1.0.94-g606058a278.nupgk

## Install library files

Install library files into your folder/project.

`> libman install jquery`

Will install the latest version of the library 'jquery' from the default provider.<br>
Will prompt for default provider if there is no defaultProvider in libman.json.<br>
Will prompt for destination if there is no defaultDestination in libman.json

`> libman install jquery@2.2.0`

Will install a specific version of the library from the default provider.<br>

Note: Syntax is _[LibraryName]@[LibraryVersion]_ for all providers except File System.

`> libman install twitter-bootstrap --destination wwwroot/lib/bootstrap`

Will install to the specified destination folder

## Restore

To download and install all files defined in the libman.json, run the _restore_ command

`> libman restore`

Will fail if there is a conflict with libraries. (ie. more than one library defined with the same library name.)

## Uninstall

`> libman uninstall jquery`

Will remove jquery files from the folder they were restored to.<br>
Will remove the library definition from libman.json

## Update

`> libman update jquery`

Will update to the latest version of the library.

`> libman update jquery --to 2.2.0`

Will update to a specific version of the library.

## Clean

`> libman clean`

Will remove from your project all files that were restored.

## Cache

### Cache List

`> libman cache list`

Will print a list of all libraries that exist in the cache - by library name only.

`> libman cache list --files`

Will print a list of all libraries that exist in the cache, listing all files in the library cache.

### Cache Clean

`> libman cache clean`

Will remove all files in the local machine's cache.

`> libman cache clean --provider cdnjs`

Will remove all files in the local machine's cache for the specified provider.