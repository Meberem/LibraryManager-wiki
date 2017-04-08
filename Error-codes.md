When installing and restoring packages, errors can occur. Here's an index over known errors.

## LIB000
Unknown error. An exception occurred that weren't handled by the individual providers.

## LIB001
Provider unknown. A unknown provider id has been specified. It could be because of a typo or a missing provider extension.

## LIB002
Unable to resolve source. This usually happens when the `id` of the library is unknown to the provider, typically due to a typo or using the wrong provider.

## LIB003
Could not write file. The host (e.g Visual Studio) was not able to write the file into the project. It could be because of missing file permissions.

## LIB004
Manifest malformed. The `library.json` file contains syntax errors.