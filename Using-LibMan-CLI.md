Here's a handy cheat sheet for getting started with LibMan CLI

## Get the LibMan global tool

Before you can use LibMan from the CLI, you must first download and install the global tool via the dotnet CLI.

`> dotnet tool install -g libman`

## Install library files

`> libman install jquery`

Will prompt for default provider if there is no defaultProvider in libman.json.<br>
Will prompt for destination if there is no defaultDestination in libman.json

`> libman install jquery@2.2.0`

Will install a specific version of the library.<br>
Note: Syntax is [LibraryName]@[LibraryVersion] for all providers except File System.

`> libman install twitter-bootstrap --destination wwwroot/lib/bootstrap`

Will install to the specified destination folder

## Restore

`> libman restore`

## Uninstall

`> libman uninstall jquery`

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

Will print a list of all libraries that exist in the cache

`> libman cache list --files`

Will print a list of all libraries that exist in the cache, listing all files in the library cache.

### Cache Clean

`> libman cache clean`

Will remove all files in the local machine's cache.

`> libman cache clean --provider cdnjs`

Will remove all files in the local machine's cache for the specified provider.