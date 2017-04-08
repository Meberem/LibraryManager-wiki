The `library.json` file is a manifest containing a list of the libraries used by the current project. It is similar to Bower's `bower.json` and npm's `packages.json` in that aspect.

## Example
This example shows a `library.json` file with 2 libraries defined - one from the [cdnjs provider](cdnjs-provider) and one from the [filesystem provider](filesystem-provider).

```json
{
  "version": "1.0",
  "defaultProvider": "cdnjs",
  "packages": [
    {
      "id": "jquery@3.2.1",
      "path": "js/lib",
      "files": [ "jquery.min.js" ]
    },
    {
      "provider": "filesystem",
      "id": "../../path/to/file.js",
      "path": "js/lib",
      "files": ["file.js"]
    }
  ]
}
```

## Reference

### version (optional)
Specifies the version of the `library.json` syntax being used on the file. The only valid value is `"1.0"` at this point, but that may change with future versions.

**Type**: string

### defaultProvider (optional)
