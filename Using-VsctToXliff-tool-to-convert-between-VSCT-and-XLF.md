There is no "standard" tool for VSCT to XLF conversion and round-tripping, so we are using a tool developed by NodeJS Tooling team. I (alexgav)tweaked the tool slightly to make the output XLF more compatible with some other XLF tooling we are using (e.g. machine translation). 

The location of the sources and binary for the tool is TBD.

Command-line usage of the tool is 

usage: ```VsctToXliff.exe <sourcefile.vsct> <xliff dir> [--generatexlf | --generatevsct].```

|option|description|
|:-- |:--|
|--generatexlf | This will create xlf files for all VS locales in the xliff dir, overwriting any existing files!|
|--generatevsct | This will create vsct files for all VS locales in the same dir as the sourecfile.vsct, overwriting any existing files!|

We may possibly further customize the tool to allow preservation of the already translated text.

## Producing XLF files

Running the tool with ```--generatexlf``` option and pointing to the English VSCT file, we generate the translation XLF files (e.g. VSCommands.ru.xlf). Once the generated XLF files are checked in into your project, it's ready to be localized by the loc team.

## Producing translated VSCT files

Once the vendors are done translating the XLF files and check them back into the project, the next step is to generate localized VSCT files from the localized XLF files. The same tool accomplishes that with the ```---generatevsct``` option. As of right now, simply replace the VSCT files in the project and rebuild.

## Setting up your project to support localized VSCT files

This is already done for LibMan, but may need to be done for a new project.

