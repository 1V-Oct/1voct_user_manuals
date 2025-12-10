# README

Those are tex files for 1V/OCT modular synthesisers

## Operations

### Building

Go to respective directory and type:

``` make ```

PDFs for all supported languages will be created in out directory

To make for specific language use language code (example for japanese):

``` LANG=jp make ```


For The Centre there is parameter BUILD_TYPE that can be either 'manual or 'refcards' to build User's Manual or Reference Cards from the same source.

``` BUILD_TYPE=refcards LANG=en make ```

### Cleaning

Go to respective directory and type:

``` make clean ```


## Translations

Translations are in respective directoriesm in 'pages' and must be named by language code. See Taipo's directory to understand more. When the file is not present in translated directory the english version of file will be used instead.