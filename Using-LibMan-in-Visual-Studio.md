This topic discusses how to use LibMan from inside Visual Studio.

# Overview of LibMan in Visual Studio

Visual Studio has built-in support for using LibMan in Web Projects, with UI tooling - including a window that helps you add files to your project, as well as rich editing support for the [LibMan manifest file](libman-manifest) (libman.json).

Though LibMan can work from any folder or any project type (via CLI or a CI build script), within Visual Studio, LibMan features are only available Web Projects.

## Getting started with LibMan

Open a Web Project in [Visual Studio 2017](https://visualstudio.com/vs) (v15.8 Preview 3 and above).

! If you're looking to get started with a new Web Project, see the [Getting Started - Razor MVC guide](getting-started-with-web).

Various elements include:
- UI components
  - Add New Library
  - Manage Client-side Libraries
  - Enable Restore on Build
  - Clean
- Editing the manifest (libman.json)
  - IntelliSense is available
- Actions
  - Install/Uninstall, Restore, Clean
  - Status shown in Background Task Center
  - Output shown in Output window