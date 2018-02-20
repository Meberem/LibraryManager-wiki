There is no "standard" tool for VSCT to XLF conversion and round-tripping, so we are using a tool developed by NodeJS Tooling team. I (alexgav)tweaked the tool slightly to make the output XLF more compatible with some other XLF tooling we are using (e.g. machine translation). 

The location of the sources and binary for the tool is TBD.

Command-line usage of the tool is 

usage: VsctToXliff.exe <sourcefile.vsct> <xliff dir> [--generatexlf | --generatevsct].
--generatexlf | This will create xlf files for all VS locales in the xliff dir, overwriting any existing files!
:-- | --:
--generatevsct | This will create vsct files for all VS locales in the same dir as the sourecfile.vsct, overwriting any existing files!