XML parser for D
================

This is my implementation of an XML parser for the D programming language. I'm no longer actively working on it, but I might review changes and accept them if you send me pull requests.


## Module mfr.range

Two functions to abstract the consumption and retention of the consumed content of a range. The 'consumeEx' function hasn't proven flexible enough for some things in mfr.xmltok however, so it currently isn't used.

Untested with ranges other than arrays.


## Module mfr.byunit

Implements frontUnit and popFrontUnit so you can easily check ASCII characters and later skip over them without triggering the UTF-8 multibyte sequence decoder.


## Module mfr.xmltok

Implements various token structs, a tokenize function (which is the actual tokenizer), a XML writer class, and a forward range for iterating over tokens.

Also provides functions for detecting a BOM and reading the xml declaration. The higher-level parser is responsible for calling these function and act accordingly, especially managing the encoding.

Most of the parsing is actually implemented in private functions called by tokenize.

Current issues:

- Would probably support wstring and dstring as input without much hassle, but tokens are defined to contain UTF-8 strings. Do we need to make tokens templated structs? Or should we wrap the whole parser (with it's token types) in one big template/struct?

Still to do:

- throw meaningful exceptions types instead of plain Exception
- adapt it so it can work with various ranges
- add unit tests for BOM and xml declaration checking.

Probably low priority:

- implement parsing of DTD internal subset
- add some sort of callback for user-defined entities


## Module mfr.xml

Implements a simple XML tree. Nothing really special about it, except that its built on mfr.xmltok;

Still to do:

- Handle BOM and encoding info in XML declaration; currently only UTF-8 is supported.
