# The executable format
## Introduction
This information is mostly based on [this blog post][1].

All executables compiled with CoolBasic (abbreviated CB from now on) are compressed with [UPX][upx_link], but you don't need to uncompress them to access the bytecode, since it's always concatenated to the end of the executable.

## Data layout
In an uncompressed CB executable the application specific data starts at offset 0x9AA00. The layout of the whole executable follows.

	[CB-runtime] (633343 bytes)
	[Garbage] (20 bytes)
	[The number of commands] (4 byte integer)
	[A useless integer] (4 byte integer)
	[The number of string literals] (4 byte integer)
	[String data]
		[string_length] (4 byte integer)
		[string_data] (string_length bytes)
	[CoolBasic bytecode]
		[The main command] (1 byte)
		[additional commands] (n bytes)
	[CB-EXE data location - 4] (4 bytes)
		
Please note that the data location is saved as an offset from the end of the file.


[1]: http://killedwhale.info/?p=43
[upx_link]: http://upx.sourceforge.net/