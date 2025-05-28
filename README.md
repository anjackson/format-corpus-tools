format-corpus-tools
===================

Tools and utilities for working with the format-corpus repo, and format signatures

## Fidget

Fidget is a command-line tool for testing and generating format identification signatures.

### Installation ###
Download the Windows or *NIX binary package from [here](https://github.com/openplanets/format-corpus-tools/downloads).  Unpack it and run the supplied script, either directly from that folder or by adding it to your PATH.

### Identifying the format of files ###

    $ fidget test.pdf
    application/pdf

### Listing supported formats ###
If you're not sure if Fidget already supports a particular format, you can find out by looking through the supported formats. To list all known formats, use this:

    $ fidget -l

and you'll get a bit tab-separated list showing MIME type, extensions, the 'name' (which is the same as the type at present) and the description (if any).  This option can be combined with the `-s` and `-A` options (see below)

### Testing new signatures ###

If you create a new signature in the Tika-compatible Mime-Info standard format ([e.g. this one](https://github.com/openplanets/format-corpus-tools/blob/master/tools/fidget/src/test/resources/org/apache/tika/mime/percipio.pdf.xml) generated using [Percipio](https://github.com/anjackson/percipio/wiki/How-to-run-Percipio)), you can test it like this:

    $ fidget -s src/test/resources/percipio.pdf.xml test.pdf
    application/pdf

By default, the new signature information is merged in with the existing signatures. If you want to avoid this, and test the signature in isolation, you can use the -A option:

    $ fidget -A -s src/test/resources/percipio.pdf.xml test.jpg
    application/octet-stream

#### Convert to DROID format ####
Fidget also contains some experimental functionality to convert Mime-Info signatures into DROID signatures. You can invoke it like this:

    $ fidget -C -s src/test/resources/percipio.pdf.xml 

Note that a live web connection is required to make this work, as it relies upon a web-based conversion service supplied by the National Archives of the UK.

### Command-line options ###

    $ fidget -?
    usage: fidget [OPTION]... [FILE]...
     -?,--help               print help message
     -A,--alone              use only the supplied signature file, do not load
                             the embedded ones
     -C,--convert-to-droid   convert supplied signature file into DROID form
     -l,--list               list all known types.
     -s,--sig-file <FILE>    use this mime-info signature file
