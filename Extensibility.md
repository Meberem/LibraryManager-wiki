
TODO: create a Visual Studio template for writing Library Installer extensions

## Step 1 
Make sure the Visual Studio SDK is installed and then create a new extensibility project by creating a _VSIX Project_.

## Step 2
Install the **Microsoft.Web.LibraryInstaller.Contracts** NuGet package

## Step 3
Implement the **IProviderFactory** and **IProvider** interfaces from the NuGet package add an `[Export(IProviderFactory)]` attribute to the **IProviderFactory** class.

## Step 4
Mark the VSIX as a MEF export by opening the .vsixmanifest file and add the project as an MEF Component under **Assets**.