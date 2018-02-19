# Library Manager Localization

Library manager localization is using industry standard XLIFF file format for localization. The supported language set is the same as for Visual Studio (cs, de, en, es, fr, it, ja, ko, pl, pt-BR, ru, tr, zh-Hans, zh-Hant). The localization is currently done by the Microsoft vendor team. The point of contact are Alex Gavrilov on the Web Tools team, and Norah Hogoboom, Praveen Kumar Kashimsetty, and Veronika Vasikova on the loc team.

## Localization Process

We will have a set of XLIFF files checked in into LibMan repo. Loc team will pick up XLIFF (.xlf) files directly from the repo for translation, and will check in the files back into the repo. We will have a separate branch for the loc team to work in to avoid possible conflicts during the check-in of the translated xlf files. 

Currently localization is scheduled on-demand. We will let the loc team know when we have new strings for them to localize. Typically loc team needs at least 1 week to loc the strings, so ideally we should let them know no less than two weeks before the release. 

## Native resources and XLIFF tools

LibMan projects will continue consuming resources in native format, such as RESX and VSCT. Various tooling is used to generate XLIFF files from native resource files, and then use translated XLIFF files to generate localized RESX and VSCT files. Satellite assemblies will be produced from the localized native resource files to be included into VSIX. 

## RESX file localization using Mutlilingual App Toolkit

