# How To Use Multilingual App Toolkit (MAT) for RESX localization

## Install MAT

The first step is to download and install MAT 4.0 from https://marketplace.visualstudio.com/items?itemName=MultilingualAppToolkit.MultilingualAppToolkit-18308 (or directly from Visual Studio by using Tools->Extensions and Updates.

![Install from VS](./images/InstallMATFromVS.png)

Once MAT is installed, you will have a new menu item under your Tools menu - "Mutlilingual App Toolkit". 

![Mutlilingual App Toolkit Menu](./images/ToolsMATMenuItem.png)

You will use that menu to enable MAT in new projects. You should not need to use it unless you are adding a new project to LibMan (or starting a completely different product/project). 

## Enable MAT in your projects (already done for LibMan)

Prior to enabling MAT, you need 

1. Add Properties\AssemblyInfo.cs if it doesn't exist in your project already
2. Add ```[assembly: NeutralResourcesLanguage("en")]``` entry to the AssemblyInfo.cs

If you don't do that, you'll get ```Project 'Microsoft.Web.LibraryInstaller.Contracts' was not enabled - the project's source culture could not be determined.``` in the Multilingual App Toolkit output window.

Once you've done the steps above, select the desired project in the Solution Explorer and use Tools->Multilingual App Toolkit->Enable Selection to enable MAT in the selected project. 

![Enable MAT](./images/EnableMAT.png)

It will modify your csproj file to add something like
```
  <PropertyGroup Label="MultilingualAppToolkit">
    <MultilingualAppToolkitVersion>4.0</MultilingualAppToolkitVersion>
    <MultilingualFallbackLanguage>en</MultilingualFallbackLanguage>
    <TranslationReport Condition="'$(Configuration)' == 'Release'">true</TranslationReport>
    <SuppressPseudoWarning Condition="'$(Configuration)' == 'Debug'">true</SuppressPseudoWarning>
  </PropertyGroup>
```

and

```
  <Target Name="MATPrerequisite" BeforeTargets="PrepareForBuild" Condition="!Exists('$(MSBuildExtensionsPath)\Microsoft\Multilingual App Toolkit\Microsoft.Multilingual.ResxResources.targets')" Label="MultilingualAppToolkit">
    <Warning Text="$(MSBuildProjectFile) is Multilingual build enabled, but the Multilingual App Toolkit is unavailable during the build. If building with Visual Studio, please check to ensure that toolkit is properly installed." />
  </Target>
```

Make sure to save your csproj at this point. You are done enabling MAT for this project. Repeat for other projects as needed. You can also run it on the solution level.

**Troubleshooting:** Look in the Output Window, and Make sure Multilinguage App Toolkit is selected. If all goes well, you should get 

```
1>  Project 'Microsoft.Web.LibraryInstaller.Contracts' was enabled.  The project's source culture is 'en' [English]. 
```

![MAT Output Window - Success](./images/MATSuccess.png)

If something goes wrong, you may get an error. Google is your friend in that case.

![MAT Output Window - Error](./images/MATError.png)

## Add Translation Languages

Once you have MAT enabled, adding translation languages is the next step. At this point, you should have a new context menu item when you select your project in Solution Explorer - Multilingual App Toolkit. Select that, and then select Add Translation Languages:

![Add Translation Languages](./images/AddTranslationLanguages.png)

You might get an error message like below

![Translation Provider Manager Issue](./images/TranslationProviderManagerIssue.png)

Click OK to dismiss it. You should get the following dialog for language selection

![Translation Languages](./images/TranslationLanguagesDialog.png)

Use it to select the desired languages. Start with German (de). You can use the Search box to type in the language name or abbreviation as shown above. Once German is shown, make sure to check its checkbox and click OK. You will get MultilingualResources folder added to your project, and your first XLF file for German translation generated from the RESX file in your project:

![Multilingual Resources Folder](./images/MultilingualResourcesFolder.png)

You will also get new German RESX file generated as well:

![Generated Translation RESX](./images/GeneratedTranslationResx.png)

Now you can bring your Add Translation Languages dialog again and finish adding all languages (cs, de, es, fr, it, ja, ko, pl, pt-BR, ru, tr, zh-Hans, zh-Hant). You can add them all at once, without dismissing the dialog. At the end, your project should look something like this:

![All Languages Added](./images/AllLanguagesAdded.png)

Check in the modified project into the loc branch in Git. At this point your project is ready for loc team vendors to pick up the XLF files.

## (Workaround) Fixup csproj to ensure localized resx file regeneration

There seems to be a bug in MAT that requires this manual step. With the current setup, localized resx files (e.g. text.ru.resx) are generated initially, but not updated afterwards. E.g. if you add a new string in the English resx file and build, you will get updated [locale].xlf files (e.g. filename.ru.xlf), but not updated resx files (i.e. filename.ru.resx remains unchanged, without the newly added string). I (alexgav) looked at how other projects using MAT are setup and noticed that they add the following in their csproj files

```
  <ItemGroup>
    <XliffResource Include="MultilingualResources\*.xlf" />
  </ItemGroup>
```

Adding that to the csproj file of your project seems to fix up regeneration of the translated resx files on build. So make sure to add it to your csproj files.

## (Optional) Machine-Translate Generated XLF files

One of the nice features of XLF is that they can be machine-translated. Simply drop the generated XLF file(s) to 

\\kimkim60\BlackBox\Hackathon\Service-CE\DROP\[your alias]\[culture] (e.g. \\kimkim60\BlackBox\Hackathon\Service-CE\DROP\alexgav\ru)

wait a minute or two, and pick them up from 

\\kimkim60\BlackBox\Hackathon\Service-CE\PICKUP\[your alias]\[culture] (e.g. \\kimkim60\BlackBox\Hackathon\Service-CE\PICKUP\alexgav\ru)

You should see translated text in the picked up XLF file. Normally vendors will manually go over the translated text and fix it up as needed. 

## Adding new resource strings

If you need to add a new resource string, the process is pretty simple (once you followed the above steps to setup your project). 

Simply add your new string to the English resx file and build. Your string should get automatically copied to all of the localized xlf files (e.g. filename.ru.xlf). MAT is smart enough to add new untranslated string to XLF files without losing all existing translations. 

Upload the xlf files to LibraryManager.Loc - https://github.com/aspnet/LibraryManager.Loc repository and let the localization team know that the files are ready for translation. 

Typically we will do it about two weeks prior to the ship date to allow sufficient time for vendors to localize the newly added items. The vendors will send a pr once the files are translated. At this point we will need to merge the changes to LibraryManager.Loc repository. 

To copy the files back to LibraryManger project, select the XLF file to update (e.g. somefile.ru.xlf) and use Multilingual App Resources context menu in Solution Explorer to execute Import/Recycle Translations... command. That will bring up - Import Translations Dialog.

Click Add, then navigate to the translated XLF file (e.g. Russian translation if you selected "filename.ru.xlf"). Once you selected the file, click "Import & Recycle" button in the dialog. You should get a message that resources were imported successfully.

Now build the project and open the translated RESX file (e.g. filename.ru.resx). You should see localized strings in your RESX file. Build the project will produce satellite assemblies to be included into the VSIX. 