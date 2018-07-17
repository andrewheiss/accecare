# accecare: Remove identifying information from manuscripts

**ac•ce•ca•re**&ensp;`/'attʃeka:re/`&ensp;*verb*&ensp;(Italian)&emsp;&emsp;**1** "to make blind"

---

**accecare** is a simple helper script that essentially takes a list of words and phrases and changes them to something else. 

It's designed to be used with Pandoc to replace identifying information in an academic manuscript with anonymized (or blinded) details. Instead of manually searching and replacing your document before compiling a blinded document (and then undoing all the blinding to compile a non-blinded document), this script takes care of anonymization for you.

## Usage

1. Create a CSV file with two columns named `original` and `replacement`. See [`replacements.csv`](replacements.csv) for an example.
1. Make `accecare.py` executable with `chmod a+x accecare.py`
1. Run `accecare.py` on a Markdown file and pipe the output to pandoc
1. That's it!

## Example

Ordinarily, you can compile [`example.md`](example.md) as an HTML file with identifying information included like so:

```sh
pandoc example.md -s --template templates/author_info.html5 -o output/example.html
```

This creates [a lovely manuscript](https://cdn.rawgit.com/andrewheiss/accecare/a0fbb937/output/example.html).

To create a blinded manuscript, you can either edit [`example.md`](example.md) by hand and remove all identifying information (boo), or pipe the output of `accecare.py` through to pandoc (yay):

```sh
./accecare.py replacements.csv example.md | pandoc -s --template templates/author_info.html5 -o output/example_blinded.html
```

This creates [a lovely anonymized manuscript](https://cdn.rawgit.com/andrewheiss/accecare/a0fbb937/output/example_blinded.html).

## Attenzione!

This is a super simple and overly crude method for blinding manuscripts. With the example [`replacements.csv`](replacements.csv), for instance, every occurrence of NASA would be replaced, even if it's just mentioned in the text.
