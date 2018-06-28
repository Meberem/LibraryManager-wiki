# Visual Studio support for LibMan

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
1. Use the "Add Client-Side Library" dialog
2. Edit the libman.json file in the root of the project

## Add Client-Side Libraries

- Choose a folder that you want to add files to (or a parent thereof).
- Right-click the folder and select **Add->Client-Side Library...**<br>
  ![Add Client-side Library via Solution Explorer context menu](https://user-images.githubusercontent.com/17131343/42005703-baa86756-7a2a-11e8-8a7b-791b75835c6a.png)

  The "Add Client-Side Library" dialog will open with focus in the **Library** field.<br>
- Type the name of a library you want to fetch (ie. "jquery", "twitter-bootstrap")<br>
  IntelliSense will provide a list of libraries starting with the name given.
- Select the correct item then press Tab.<br>
  The library ID will be completed with the "@" symbol followed by the latest version known to that provider.<br>
  Focus will move to the files selection radio buttons.
- To include all files in the specified library, set the radio button to "Include all library files".
- To specify a smaller set of files from the library, choose the "Choose specific files:" option, which will enable the file selector tree with a smaller set selected by default.<br>
  Use the checkboxes to the left of the files to select the files to download.
![Add Client-Side Library dialog with query files selected](https://user-images.githubusercontent.com/17131343/41642784-2499ab88-741e-11e8-9b62-db503d17b660.png)
- Specify the location of the new files within your web project. (Where do you want the files to go?)<br>
  Note: It is recommended to keep each library in a separate folder. The default location suggested for the new files will be a folder with the same name as the library under the directory the dialog was launched from.<br>
  Modify the **Target Location** as necessary.
- Press **Install**.<br>
  The configuration will be written to libman.json in the project root and the files will be downloaded into the project.<br>
![Web project in Solution Explorer with libman.json and jquery files added](https://user-images.githubusercontent.com/17131343/41643578-72bee682-7420-11e8-8008-66dfac003f6a.png)
- Messages will appear in the Output window
![Library Manager output in the Visual Studio Output window](https://user-images.githubusercontent.com/17131343/41643377-d6e4e32e-741f-11e8-9d64-9b62a952f2af.png)

## Edit the LibMan Manifest (libman.json)

All LibMan operations are based on the content of the LibMan manifest, which is the libman.json at the root of the project.

You can manually edit this file to define the library files that should be downloaded into the project.

Visual Studio offers editing support for the libman.json file, including coloring, formatting, IntelliSense and schema validation.

![Editing libman.json in Visual Studio](https://user-images.githubusercontent.com/17131343/41644228-4a552b50-7422-11e8-9a14-0704b5a60f17.png)

Note: LibMan only supports one version of each library from each provider. The libman.json file will be invalid if it contains two libraries with the same library name for a given provider.

# LibMan Operations

There are several Library Manager operations you can perform with Visual Studio.
Some actions are available from the context menu on the LibMan config file (libman.json)

![LibMan operations available on libman.json context menu](https://user-images.githubusercontent.com/17131343/42006690-473b4bac-7a30-11e8-8739-554995484f72.png)

## Restoring library files into your project

If your project has a valid LibMan config file (libman.json), the **Restore Client-Side Libraries** operation will download all the defined library files and place them in your project at the locations specified for each library.

While the operation is running, the Task Status Center icon on the status bar will be animated. Clicking the icon will open a pop-up window listing the known background tasks.<br>
Messages will be sent to the Library Manager feed in the Output window as well as the status bar.

## Clean library files from your project

The **Clean Client-Side Libraries** operation will remove all the library files that were previously restored by LibMan in Visual Studio. So that additional non-library files are not unintentionally removed, the Clean operation will not delete whole directories. It will only remove the files that were included in the previous restore.

## Enable Restore Client-Side Libraries on Build

If you'd like the project to be configured so that it automatically triggers a LibMan Restore operation whenever the project is built, you can choose to **Enable Restore Client-Side Libraries on Build...".<br>
This will download a NuGet package and add it to your project so LibMan will run as part of the build operation for that project.

![Enable Restore On Build: Adds a NuGet package to your project](https://user-images.githubusercontent.com/17131343/42007019-49bb0546-7a32-11e8-9e63-5cb48c791121.png)

## UI Elements
Various elements include:
- Menu items
  - Add->Client-side Library
  - Restore Client-side libraries (Project/Solution)
  - Manage Client-side Libraries
  - Enable/Disable Restore on Build
  - Clean
- UI
  - Add Client-Side Library dialog
- Editing the manifest (libman.json)
  - IntelliSense is available
- Actions
  - Install/Uninstall, Restore, Clean
  - Enable/Disable Restore on build
    - Triggers NuGet download
  - Status shown in Background Task Center
  - Output shown in Output window
  - Output shown on status bar