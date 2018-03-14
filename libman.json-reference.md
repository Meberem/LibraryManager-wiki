The `libman.json` file is a manifest containing a list of the libraries used by the current project. It is similar to Bower's `bower.json` and npm's `packages.json` in that aspect.

## Example
This example shows a `libman.json` file with 2 libraries defined - one from the [cdnjs provider](cdnjs-provider) and one from the [file-system provider](file-system-provider).

```json
{
  "version": "1.0",
  "defaultProvider": "cdnjs",
  "defaultDestination": "js/lib",
  "libraries": [
    {
      "library": "jquery@3.2.1",
      "files": [ "jquery.min.js" ]
    },
    {
      "provider": "filesystem",
      "library": "../../path/to/file.js",
      "destination": "js/files",
      "files": ["file.js"]
    }
  ]
}
```

## Reference

### version (optional)
Specifies the version of the `libman.json` syntax being used on the file. The only valid value is `"1.0"` at this point, but that may change with future versions.

**Type**: string

### defaultProvider (optional)
Use this field to specify a default provider to avoid having to specify the provider in the individual library entries (see below). If a package has a `"provider"` property specified, then that will always win over the `"defaultProvider"`.

**Type**: string

### defaultDestination (optional)
Use this field to specify a default destination to avoid having to specify the destination in the individual library entries (see below). If a package has a `"destination"` property specified, then that will always win over the `"defaultDestination"`.


**Type**: string (a valid provider id)

### libraries
This is an array of objects describing an individual library.

**Type**: array of library objects

### libraries.provider
A string matching the id of a known provider. This field is required if the root property `"defaultProvider"` is not set.

**Type**: string

### libraries.library (required)
The `library` is a identifier for a library that is uniquely identifiable by the specified provider.

**Type**: string

### packages.destination (required)
The destination is a folder path relative to the `libman.json` file. It represents the folder you want the library files copied to.

**Type**: string

### packages.files (required by some providers)
The files array is a list of files from the individual library you wish to copy to your project. It allows you to copy just the files from the library you need. Some providers leaves the `files` array optional which means that when not specified, all files from the library will be copied to the project.

**Type**: array of string