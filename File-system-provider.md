Please see the [libman.json reference](library-json-reference) for more details.

## filesystem reference
Here are some specifics about the filesystem provider when used from the `libman.json` file.

### provider
Nothing specific to filesystem.

### id (required)
The filesystem provider allows you to copy files from local file system, network drives and custom URIs. Here are some examples of what `id` can look like:

- absolute file path: _c:\path\to\file.js_
- relative file path: _folder/file.js_
- relative file path: _../../my/file.js_
- absolute folder path: _c:\my\folder_
- relative folder path: _my/folder_
- Url: _http://example.com/my/file.js_

### path (required)
Nothing specific to cdnjs.

### files (required)
If the `id` property points to a folder, then the files array must contain one or more file names matching files in that folder. if `id` points to a URI or a single file then the files array must contain a single entry and the value is any file name you wish to use.

**Type**: Array of strings