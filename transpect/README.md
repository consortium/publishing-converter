# XProc-based document transformation / checking

 * Converts HTML to EPUB, IDML to HTML and to EPUB and back… more coming soon;
 * applying Schematron checks to the input, to intermediate formats, and to the output;
 * rendering the checking reports as HTML
 * generating other formats, such as EPUB

## Prerequisites

 * ext (see http://nopugs.com/ext-tutorial)
 * Java 1.7 or newer

## Initial Checkout

    git clone --recursive https://github.com/consortium/BinB

In ```transpect``` folder, call:

    ext co

## Updates

Whenever you want to use transpect, you need to be up-to-date. 
Call:

    git submodule update --recursive

Then call:

    ext up

## Sample invocation

This invokes a simplistic IDML→HTML→EPUB pipeline that doesn’t attempt at identifying any 
structure in the input (other pipelines are in preparation). 
In the ```transpect``` folder, call:

    calabash/calabash.sh -o html=out.html -o raw-html=raw.html -o hub=/dev/null adaptions/common/xpl/idml2epub.xpl debug=yes debug-dir-uri=file:$(readlink -m debug) input=../content/sample/idml/sample.idml

The EPUB will then be created as ../content/sample/sample.epub

If you’re on a Mac and if you didn’t install the GNU version of readlink, you might have to specify the absolute path yourself.

If you specify ```debug-dir-uri=debug```, it might be that the debug files are stored in xproc-util/store-debug/xpl/debug. 
Relative paths for the IDML input should work fine though.

Command for Mac users:

    calabash/calabash.sh -o html=out.html -o raw-html=raw.html -o hub=/dev/null adaptions/common/xpl/idml2epub.xpl debug=yes debug-dir-uri=file:$(pwd)/debug input=../content/sample/idml/sample.idml

Cygwin example:

    calabash/calabash.sh -o html=out.html -o raw-html=raw.html -o hub=$(cygpath -ma /dev/null) adaptions/common/xpl/idml2epub.xpl debug=yes debug-dir-uri=file:/$(cygpath -ma ../debug) input=../content/sample/idml/sample.idml

### HTML → EPUB pipeline

The pipeline ```idml2epub.xpl``` invokes another pipeline, ```html2epub.xpl```, that you may also invoke directly:

    calabash/calabash.sh -i source=edited.html -o html=/dev/null adaptions/common/xpl/html2epub.xpl

Please note that this is for HTML input that is also well-formed XML. For the general case of HTML5, there is a different
pipeline that uses validator.nu to parse the file:

    calabash/calabash.sh -o raw-html=input.xhtml adaptions/common/xpl/html5_2epub.xpl input=input.html
 

## Documentation

HTML pages of the embedded XProc documentation may be generated with the following command line invocation: 

    calabash/calabash.sh -i source=adaptions/common/xpl/idml2epub.xpl transpectdoc/xpl/transpectdoc.xpl project-name=BinB

The documentation will be stored in the doc subdirectory. This may be overridden with the option output-base-uri=… (may also be a relative path).
