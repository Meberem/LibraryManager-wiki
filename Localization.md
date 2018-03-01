# Library Manager Localization

Library manager localization is using industry standard XLIFF file format for localization. The supported language set is the same as for Visual Studio (cs, de, en, es, fr, it, ja, ko, pl, pt-BR, ru, tr, zh-Hans, zh-Hant). The localization is currently done by the Microsoft vendor team. The point of contact are Alex Gavrilov on the Web Tools team, and Norah Hogoboom, Praveen Kumar Kashimsetty, and Veronika Vasikova on the loc team.

## Localization Process

We will have a set of XLIFF files checked in into LibMan repo. Loc team will pick up XLIFF (.xlf) files directly from the repo for translation, and will check in the files back into the repo. We will have a separate branch for the loc team to work in to avoid possible conflicts during the check-in of the translated xlf files. 

Currently localization is scheduled on-demand. We will let the loc team know when we have new strings for them to localize. Typically loc team needs at least 1 week to loc the strings, so ideally we should let them know no less than two weeks before the release. 

## Native resources and XLIFF tools

LibMan projects will continue consuming resources in native format, such as RESX and VSCT. Various tooling is used to generate XLIFF files from native resource files, and then use translated XLIFF files to generate localized RESX and VSCT files. Satellite assemblies will be produced from the localized native resource files to be included into VSIX. 

## RESX file localization using Mutlilingual App Toolkit

RESX files will be localized using Multilingual App Toolkit (MAT). It's installed as an extension for Visual Studio 2017 from 

https://marketplace.visualstudio.com/items?itemName=MultilingualAppToolkit.MultilingualAppToolkit-18308

(or from within Visual Studio). 

It was selected since a number of Microsoft DevDiv open source projects successfully utilize it (e.g. Microsoft.VisualStudio.Threading library, etc., see https://github.com/Microsoft/vs-threading). It's a well-established product and allows round-tripping between resx <-> xls with relative ease. 

Please see [Using MAT for RESX to XLIFF conversion](Using-MAT-for-RESX-to-XLIFF-conversion) for details of translation.

## VSCT file localization using VsctToXliff tool

Unfortunately VSCT file format is not support by the MAT 4.0 tool (or any other publicly available tool for that matter). So we chose to utilize VsctToXliff tool written by NodeJS Tooling team. See https://github.com/Microsoft/nodejstools/tree/v1.3.x/Common/Tools/VsctToXliff
 for the original sources. I (alexgav) made slight changes to the tool to make generated xlf machine-translatable and editable with MAT Editor. The location of the modified sources is common\tools\VsctToXliff. See

[Using Using-VsctToXliff tool to convert between VSCT and XLF](Using-VsctToXliff-tool-to-convert-between-VSCT-and-XLF)

## Building the localized VSIX

Building the localized VSIX is unfortunately a bit complicated since LibMan projects use the new csproj file format, which doesn't include many of the standard C# targets that VSIX build tasks expect to exist. For example, SatelliteDllsProjectOutputGroup target doesn't exist in the new project system. So we will have to do some manual customization of our VSIX csproj to allow inclusion and deployment of the satellite DLLs.