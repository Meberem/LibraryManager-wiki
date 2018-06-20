## What is Library Manager (LibMan)?

LibMan is a tool that helps you download common web libraries from the Internet and include them in your web project.

Library Manager (“LibMan” for short) is Visual Studio’s client-side library acquisition tool. It's goal is to provide a lightweight, simple mechanism that helps users find and fetch common library files from external sources (such as CDNJS or UnPkg) and place them in the right location within your web application.

![Library Manager in Visual Studio 2017](https://user-images.githubusercontent.com/17131343/41626712-fb1e273a-73d1-11e8-84b4-fe623d067143.png)

### Why use LibMan?
* If your project does not require additional tools (like Node, npm, Gulp, Grunt, WebPack, etc) and you simply want to acquire a couple of files, then LibMan might be for you.
* LibMan lets you specify exactly where the files should be placed inside your project. (No additional build tasks or manual file copying required!)
* LibMan provides the benefit of a much smaller footprint in your web project as it only downloads the files you need.
To learn more about the benefits of LibMan, check out this clip of [Mads Kristensen talking about the initial prototype](https://channel9.msdn.com/Events/Build/2017/B8073#time=43m34s) in his talk at Microsoft Build 2017.

### What LibMan is not
LibMan is not a package management system. If you’re happily using npm/yarn/(or something else), we encourage you to continue doing so. LibMan was not developed as a replacement for these tools.

## How to Acquire and Install

LibMan tooling comes as part of the Web Development workload in Visual Studio 2017.<br>
Download [Visual Studio 2017](https://www.visualstudio.com/vs/) and choose the "Web Development" workload during installation (or modify an existing instance of Visual Studio 2017).

The LibMan Command Line Interface (DotNet CLI tool) can be used separately and can be downloaded from NuGet.

## How to use Library Manager (LibMan)

See the following pages for information on how to use LibMan in the various supported scenarios.

- [Using LibMan in Visual Studio](Using-LibMan-in-Visual-Studio)
- [Using LibMan from the Command Line (LibMan CLI)](Using-LibMan-with-CLI)
- [Using LibMan in a CI build](Using-LibMan-in-a-CI-Build)

## Reference

### LibMan Manifest (libman.json)
- [libman.json reference](libman.json-reference)

### Providers
- What are providers? How to choose?
- [Cdnjs](cdnjs-provider)
- UnPkg
- [File system](file-system-provider)

### Other References
- [Error codes](error-codes)
- [Extensibility](Extensibility)
- [Localization](Localization)