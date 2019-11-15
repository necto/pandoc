# GitHub Action to Convert Documents via Pandoc

This action lets you use [pandoc](https://pandoc.org/), the **swiss army knife of document conversion**.

It is based on the [`pandoc/latex`](https://hub.docker.com/r/pandoc/latex/) docker image and thus ships with LaTeX, so you can also convert right through to PDF.

The action currently uses pandoc 2.6 and will be upgrade periodically. 
If you would like to see an upgrade, please [file an issue](http://github.com/maxheld83/pandoc/issues).


## Inputs

None.


## Outputs

None.


## Secrets

None.


## Environment Variables

None.


## Example Usage

The string passed to `pandoc-args` gets appended to the [`pandoc` command](https://pandoc.org/MANUAL.html).
The whole command is interpreted by the `sh` shell, so you can use globs (e.g. `source/*.md`) to specify your inputs.

```
name: Document Conversion

on: [push]

jobs:
  convert_to_pdf:
    name: Produce the PDF with Pandoc
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v1
      - run: mkdir output
      - uses: necto/pandoc@master
        with:
          pandoc-args: "--pdf-engine=xelatex --output=output/README.pdf README.md"
      - uses: actions/upload-artifact@master
        with:
          name: output
          path: output
```
