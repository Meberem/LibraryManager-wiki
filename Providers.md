# cdnjs

The cdnjs provider uses the curated cdnjs CDN, allowing access to many FOSS libraries.  See https://cdnjs.com/ for more information about the CDN.

This provider uses the `library@version` syntax to identify each library in the manifest.

# jsdelivr

The JSDelivr provider uses the JSDelivr CDN, which mirrors any NPM package as well as provides access to libraries directly through GitHub.  JSDelivr also provides minimized versions of any JS or CSS files if they don't already exist.  See https://www.jsdelivr.com/ for more information about the CDN.

This provider uses the `library@version` syntax for NPM packages, and `@scope/library@version` for scoped NPM packages (note the leading `@`).  The value `latest` can be used as the version to always fetch the latest released version of the library.

To use GitHub as a source, the syntax is `user/project@version` where version can be either a release or a commit hash.

# unpkg

The Unpkg provider uses the Unpkg CDN, which mirrors any NPM package.  See https://unpkg.com/ for more information about the CDN.

This provider uses the `library@version` syntax for NPM packages, and `@scope/library@version` for scoped NPM packages (note the leading `@`).  The value `latest` can be used as the version to always fetch the latest released version of the library.

# filesystem

The filesystem provider allows copying files from a local or remote file path.  When the source is a single file, this provider also allows renaming the file at the destination.

This provider uses a file or folder path as the `id`.  If the `id` property points to a folder, then the `files` array must contain one or more file names matching files in that folder (i.e. selecting which files to copy). If `id` points to a URI or a single file then the `files` array must contain a single entry and the value is the file name that it will be copied to (i.e. renaming the file).