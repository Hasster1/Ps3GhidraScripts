
# Ps3GhidraScripts

A collection of scripts for parsing PS3 executables with Ghidra.

Relocations are not currently supported.

When loading a prx/elf into Ghidra be sure to select the following language (By default this is the one under the automatic selection when the recommended checkbox is disabled)
```
PowerPC:BE:64:A2ALT-32addr:default
```

## Required change
To avoid issues with decompliation the following change is needed in Processors\PowerPC\data\languages\ppc_64_32.cspec

Add `<register name="r2"/>` to the `<unaffected>` list

## Possible problems
Some cell specific instructions are currently not supported in ghidra, these are the vector store/get lvlx etc, these appear in games and may break decompilation currently.

## AnalyzePs3Binary.java
The main script, this should be used BEFORE analysis is run on the program.

This will ask for the location of the nids.txt file.

It will then parse the infomation sections and define imports/exports and name the ones it can from the nids file, and then set the TOC.

After this you should run the auto analysis tool within ghidra, and then run the syscall define script.

## DefinePs3Syscalls.java
Does what it says on the tin.

Resolves ps3 syscalls to the correct name and defines functions for them.

Should be ran after AnalyzePs3Binary and auto analysis have completed.
