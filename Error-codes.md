When installing and restoring packages, errors can occur. Here's an index over known errors.

## LIB000
Unknown error. An exception occurred that wasn't handled by the individual providers.

## LIB001
Provider unknown. A unknown provider id has been specified. It could be because of a typo or a missing provider extension.

## LIB002
Unable to resolve source. This usually happens when the `id` of the library is unknown to the provider, typically due to a typo or using the wrong provider.

## LIB003
Could not write file. The host (e.g Visual Studio) was not able to write the file into the project. It could be because of missing file permissions.

## LIB004
Manifest malformed. The `libman.json` file contains syntax errors.

## LIB005
The `"destination"` property is undefined in the `libman.json` file.

## LIB006
The `"library"` property is undefined in the `libman.json` file.

## LIB007
The `"provider"` property is undefined in the `libman.json` file.