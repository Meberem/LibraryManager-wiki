TODO: create a Visual Studio template for writing Library Installer extensions

It's easy to write your own providers for the Library Installer.

# Basic provider
A basic provider allows libraries to be installed and removed. This is all you need to provide basic functionality for your provider.

## Step 1 
Make sure the Visual Studio SDK is installed and then create a new extensibility project by creating a _VSIX Project_.

## Step 2
Install the **Microsoft.Web.LibraryInstaller.Contracts** NuGet package

## Step 3
Implement the **IProviderFactory** and **IProvider** interfaces from the NuGet package and add an `[Export(IProviderFactory)]` attribute to the **IProviderFactory** class.

## Step 4
Mark the VSIX as a MEF export by opening the .vsixmanifest file and add the project as an MEF Component under **Assets**.

# Advanced provider
Contains the same steps as in the _Basic provider_. The advanced provider will give Intellisense in `library.json`, update checks and other features.

## Step 1
Implement **ILibraryCatalog** and the other interfaces used by it.

## Step 2
Return an instance of the **ILibraryCatalog** from the **IProvider.GetCatalog** method.
