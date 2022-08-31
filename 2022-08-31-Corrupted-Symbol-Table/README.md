Background: Ghidra 10.1.5 on Windows 11, Java Oracle Version 8, update 341

~4 MB MIPS-32 binary; symbol table size: ~170K

I notice that sometimes the symbol table is corrupted during the process of assigning new names to functions and data.

Specifically, updating the name of a function/data name always seems to correctly updates that function/data name, but, occasionally, it also renames another (unrelated) function/data name to the same label.  Comes to light on inspection, or in finding a symbol associated with two or more functions.

As an example of this bug, here is a scenario, where I try to dereference a function and find that another function is (erroneously) associated with that name. 

The C-source-code inspector lists a function as "get_video_duration_from_enum()" (photo1, see highlighted function); but when I double-click on this line, I am taken to a different function "appAWBALGLib_WBParamSet()" (photo2). 

A look a the symbol table for "get_video_duration_from_enum (photo 3), shows that the symbol is associated with two functions, the correct one at 0x8005d394; and an incorrectly associated function at 0x8000f4f4

Note that this happened after I changed the name (or possibly argument type?) of "get_video_duration_from_enum", but did not touch "appAWBALGLib_WBParamSet().

The extent of this bug seems limited, and I seem to be able to fix the inconsistencies by removing unwanted associations with the symbol table editor. 
