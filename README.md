# Nim-gdb
GDB pretty printing for Nim language.
Currently, this script requires latest devel Nim compiler installed manually from:
https://github.com/nim-lang/Nim

## Usage 
Compile your nim project with `nim c -d:debug --debugger:native your_project.nim` command. Copy nim.py next to your project's executable you have just built. Start gdb debugging session with `gdb your_project`. In gdb command line run the following command to load debug helpers: `python execfile("nim.py")`

### Python 3
If your gdb is linked against python3, use the 2to3 version like so: `python exec(open("nim3.py").read())`

## Supported features:
* Type pretty printing, using ``whatis`` gdb command 
* New gdb command `$` for invoking Nim's `$` stringify operator
* New function `$dollar`, does the same `$` command but available in expressions
* Value pretty printing, including: enums, sets, seqs, strings, tuples and objects with discriminating unions

## Known Limitations:
* Printing of enum values is using reprEnum function of Nim, you need to make that this function is not removed by dead code elimination. Add `echo enumValue` line to your code anywhere to make sure reprEnum is used.
* Printing of set values is using Nim's `proc $[T](x: set[T]): string`. Given it is generic proc, you need to 
to add `echo` for every set type in use to make it available in gdb.

These limitations are planned to be resolved in the future.
