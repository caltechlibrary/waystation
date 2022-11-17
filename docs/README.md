# Waystation user documentation

This directory contains the user documentation for Waystation. The rest of this page describes how to (re)create the formatted Waystation user documentation.

## Building the docs locally

First, install [MyST](https://myst-parser.readthedocs.io/en/latest/index.html) and [Sphinx](https://www.sphinx-doc.org):

```sh
python3 -m pip install "myst-parser[linkify]"
python3 -m pip install sphinx-material
python3 -m pip install sphinx-autobuild
```

After that, rebuilding the docs should be simply a matter of running `make html` in the current directory:

```sh
make html
```

The output will be put in [`_build/html`](_build/html).  Instead of running `make` deliberately, you can also get auto-rebuilds and live preview using `sphinx-autobuild` by running the following command in the current directory (preferably in a new terminal window, because it will generate continuous output):

```sh
make auto
```


## Writing documentation

This documentation is written in [MyST-flavored Markdown](https://myst-parser.readthedocs.io/en/latest/) and the [Napoleon](https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html) extension to Sphinx.  What this means is that the documentation is written in Markdown (not reStructuredText), with essentially all the features of Sphinx and reStructuredText having MyST equivalents and some additional features &ndash; things like [pandoc](https://pandoc.org)-style footnotes, LaTeX math, and more.
