This topic discusses how to use LibMan from inside Visual Studio.

# Overview of LibMan in Visual Studio

Visual Studio has built-in support for using LibMan in Web Projects, including:

- support for configuring and running LibMan restore operation on build
- menu items for triggering LibMan **restore** and **clean** operations
- dialog that helps you search for libraries and add the files to your project
- editing support for the [LibMan manifest file](libman-manifest) (libman.json)

Though LibMan can work from any folder or any project type (via CLI or a CI build script), within Visual Studio, LibMan features are only available Web Projects.

## Getting started with LibMan

Open a Web Project in [Visual Studio 2017](https://visualstudio.com/vs) (v15.8 Preview 3 and above).

! If you're looking to get started with a new Web Project, see the [Getting Started - Razor MVC guide](getting-started-with-web).

You can add files to your web project two ways:
1. Use the "Add Client-Side Libraries" dialog
2. Edit the libman.json file in the root of the project

## Add Client-Side Libraries

- Choose a folder that you want to add files to (or a parent thereof).
- Right-click the folder and select **Add->Client-Side Libraries...**<br>
  The "Add Client-Side Libraries" dialog will open with focus in the **Library** field.<br>
- Type the name of a library you want to fetch (ie. "jquery", "twitter-bootstrap")<br>
  IntelliSense will provide a list of libraries starting with the name given.
- Select the correct item then press Tab.<br>
  The library ID will be completed with the "@" symbol followed by the latest version known to that provider.<br>
  Focus will move to the files selection radio buttons.
- To include all files in the specified library, set the radio button to "Include all library files".
- To specify a smaller set of files from the library, choose the "Select library files" option, which will enable the file selector tree with a smaller set selected by default.<br>
  Use the checkboxes to the left of the files to select the files to download.

![Add Client-Side Libraries dialog with query files selected](https://user-images.githubusercontent.com/17131343/41642784-2499ab88-741e-11e8-9b62-db503d17b660.png)

- Specify the location of the new files within your web project. (Where do you want the files to go?)<br>
  Note: It is recommended to keep each library in a separate folder. The default location suggested for the new files will be a folder with the same name as the library under the directory the dialog was launched from.<br>
  Modify the **Target Location** as necessary.
- Press **Install**.<br>
  The configuration will be written to libman.json in the project root and the files will be downloaded into the project.<br>
- Messages will appear in the Output window
![Library Manager output in the Visual Studio Output window](https://user-images.githubusercontent.com/17131343/41643377-d6e4e32e-741f-11e8-9d64-9b62a952f2af.png)

## UI Elements
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