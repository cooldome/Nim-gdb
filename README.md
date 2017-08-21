# Nim-gdb
GDB pretty printing for Nim language
Currently, this script requires patching Nim compiler using the following pull request:
https://github.com/nim-lang/Nim/pull/6240

## Usage 
Copy nim.py from this project next to executable you plan to debug. Next after loading executable, 
issue the following command in gdb: `python execfile("nim.py")`

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
