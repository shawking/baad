![baad logo](https://github.com/dfalster/baad/raw/master/extra/baad.png)

# Setup


## dataMashR

This compilation requires package ['dataMashR'](https://github.com/dfalster/dataMashR), which is still under development.

To ensure we use the right version of dataMashR we are using using git's [submodules feature](http://git-scm.com/book/en/Git-Tools-Submodules).

To setup existing submodules after cloning run

    git submodule init

To update submodule to correct version:

    git submodule update

You can then install the package locally (into the folder `/lib`) by running

    make install-dataMashR

## Other packages

Other packages required are,

    knitr, gdata, bibtex, knitr, knitcitations, plyr, mvbutils, whisker

If you are going to lookup species names from Taxonstand and taxize (with the postProcess function), you will also need,

    taxize, Taxonstand, jsonlite

All these packages are available from CRAN.


# Line endings

## Fix all line endings

We have had problems with Excel on OS X [which uses old line endings](http://developmentality.wordpress.com/2010/12/06/excel-2008-for-macs-csv-bug/), which tend to obscure diffs.  To avoid this problem, please set up a git hook that checks for line endings by running (in the project root directory)

	ln -s ../../scripts/check_line_endings.sh .git/hooks/pre-commit

This will check that all files have unix endings once files have been staged (so after git's `crlf` treatment).  You can run it manually to check by running

	./scripts/check_line_endings.sh

which looks at staged files only, or

	./scripts/check_line_endings.sh csv

which looks at *all* csv files in the project, including uncommitted, unstaged, ignored files, etc.

To *fix* line endings, run

	./scripts/fix-eol.sh path/to/file.csv

To fix *all* files in the project, run

	./scripts/fix-eol-all.sh

which looks at all csv files, regardless of git status, ending correctness, etc.  It takes a few seconds to run.

## Windows users

In addition to the issue described above, Windows users must make sure that git is configured to commit with Unix-style line endings. This maintains the integrity of files on a Windows machine, while making sure the line-endings in the repository can be used by Mac (Unix) and Windows users alike.

When installing git-scm, make sure the setting
  
    Checkout Windows-style, commit unix-style line endings

is checked (the default).


# Rebuilding the database

The database can be rebuilt using the Makefile. Simply run,

    make

This will rebuild the database, stored in `output/baad.rds`. To read this dataframe in `R`, use `readRDS`,

    dat <- readRDS('output/baad.rds')

**Windows users** must install a bundle of Unix-like tools (otherwise `make` is not available). These are conveniently wrapped in [Rtools](http://cran.r-project.org/bin/windows/Rtools/) (select the newest version and install).

The database is stored as a list with components `data`, `contact` and `ref`. These contain the data (as a dataframe), contact information for the data providers, and references to publications (where available).















