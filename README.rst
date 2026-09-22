|version| |licence| |released|

.. |version| image:: https://img.shields.io/github/v/tag/AndrewMathas/git-ldiff?color=success&label=git-ldiff
   :alt: Latest version

.. |licence| image:: https://img.shields.io/badge/licence-GPL--3.0-blue?style=flat-square
   :alt: GNU General Public License, Version 3, 29 June 2007
   :target: https://www.gnu.org/licenses/gpl-3.0.html

.. |released| image:: https://img.shields.io/github/release-date/AndrewMathas/git-ldiff?label=released&color=red
   :alt: Release date

======================
git-ldiff and git-lpdf
======================

A python script for producing PDF files from a git repository that tracks
LaTeX documents. There are two modes:

- ldiff: uses latexdiff to produce a PDF that highlights the differences
  between two commits
- lpdf:  produces a PDF file for a given commit in the repository

In both cases the commit information is printed as a banner down the
left-hand margin of every page of the PDF. This script is partially
motivated by the script git-latexdiff_ and my attempts to get it to work the
way that I wanted. The script should be used from inside a git repository.

The main idea of the script is to provide an easy way to produce a PDF file
from a git repository that is clearly annotated with the commit data. For
example, using latexdiff_, the command

.. code-block:: bash

   > git ldiff <commit>

produces a PDF file that highlights the differences between the commit
<commit> and the current working copy, and

.. code-block:: bash

   > git ldiff <commit1> <commit2>

produces a PDF file showing the differences between two commits. Similarly,

.. code-block:: bash

   > git lpdf <commit>

produces a PDF file for the commit <commit> of the main LaTeX file in the
current repository.

Unlike the original bash implementation, LaTeX documents that are spread
over several directories are fully supported: the directory structure of the
repository is preserved when the files are extracted and LaTeX is run in the
directory containing the main file, so that relative \input and
\includegraphics paths resolve correctly.

Andrew Mathas June 2014
Claude port to python September 2026

Installation
------------

Clone the git repository, or download the script, and then type either:

.. code-block:: bash

  ./git-ldiff --install [directory]   # directory defaults to $HOME/bin

or

.. code-block:: bash

  ./git-ldiff --linkinstall [directory]   # directory defaults to $HOME/bin

The first version copies the script to <directory>/git-ldiff and creates a
link from <directory>/git-lpdf to <directory>/git-ldiff. The second variation
creates two links to the script in its current location, which is useful if
you have cloned the git repository for git-ldiff.

The script makes use of the background_ package, latexmk_ and latexdiff_.
All three are available from ctan_ and are installed automatically with
TeXLive.

Usage for the ldiff script
--------------------------

::

  usage: git ldiff [-h] [-b BANNER] [-d] [-l LATEX] [--latex-opt OPT]
                   [-m TEXFILE] [-n] [-o COMMAND] [--output PATH] [-t DIR] [-k]
                   [-s] [-S] [-T TYPE] [--add-colour RGB] [--install [DIR]]
                   [--linkinstall [DIR]] [--readme]
                   [OLD] [NEW]
  
  Produce a PDF showing the differences between two versions of a LaTeX document
  in a git repository, with the versions being compared printed down the margin
  of every page.
  
  positional arguments:
    OLD                   the older version [HEAD]
    NEW                   the newer version [the working copy]
  
  options:
    -h, --help            show this help message and exit
    -b, --banner BANNER   the banner printed in the left-hand margin
    -d, --debug           print what the script is doing
    -l, --latex LATEX     the latex executable [pdflatex]
    --latex-opt OPT       an option passed to latex, repeatable; options that
                          start with a dash need the equals form: --latex-
                          opt=-shell-escape
    -m, --main TEXFILE    the main latex file
    -n, --nocleaning      keep the temporary directory
    -o, --open COMMAND    the command used to open the PDF ("" to not open it)
    --output PATH         where to write the PDF [beside the latex file]
    -t, --tmp DIR         the temporary directory used for building
    -k, --keep            keep the latexdiff LaTeX file
    -s, --safe            more robust diff of mathematics
    -S, --verysafe        very robust diff of mathematics
    -T, --latexdiff-type TYPE
                          the type of diff used by latexdiff [CULINECHBAR]
    --add-colour RGB      rgb colour for added text, "" to leave it blue
                          [0.13,0.545,0.13]
    --install [DIR]       install the script into DIR [$HOME/bin]
    --linkinstall [DIR]   link to the script from DIR [$HOME/bin]
    --readme              regenerate README.rst
  
  examples:
    git ldiff                    compare the last commit with the working copy
    git ldiff <commit>           compare <commit> with the working copy
    git ldiff <commit1> <commit2>
    git ldiff <directory> HEAD   compare a copy of the repository with HEAD
  
  OLD and NEW are commits, or `--` for the working copy, or a directory holding
  a copy of the repository. If latexdiff struggles with your mathematics then try
  the --safe and --verysafe options.

Usage for the lpdf script
-------------------------

::

  usage: git lpdf [-h] [-b BANNER] [-d] [-l LATEX] [--latex-opt OPT]
                  [-m TEXFILE] [-n] [-o COMMAND] [--output PATH] [-t DIR]
                  [--install [DIR]] [--linkinstall [DIR]] [--readme]
                  [COMMIT]
  
  Produce a PDF of a LaTeX document in a git repository, with the commit
  information printed down the margin of every page.
  
  positional arguments:
    COMMIT               the commit to typeset [the working copy]
  
  options:
    -h, --help           show this help message and exit
    -b, --banner BANNER  the banner printed in the left-hand margin
    -d, --debug          print what the script is doing
    -l, --latex LATEX    the latex executable [pdflatex]
    --latex-opt OPT      an option passed to latex, repeatable; options that
                         start with a dash need the equals form: --latex-
                         opt=-shell-escape
    -m, --main TEXFILE   the main latex file
    -n, --nocleaning     keep the temporary directory
    -o, --open COMMAND   the command used to open the PDF ("" to not open it)
    --output PATH        where to write the PDF [beside the latex file]
    -t, --tmp DIR        the temporary directory used for building
    --install [DIR]      install the script into DIR [$HOME/bin]
    --linkinstall [DIR]  link to the script from DIR [$HOME/bin]
    --readme             regenerate README.rst
  
  examples:
    git lpdf                     PDF of the current working copy, date stamped
    git lpdf b675cdf             PDF of the main LaTeX file as of commit b675cdf
    git lpdf --main paper/ms.tex HEAD~3
    git lpdf <directory>         PDF of the copy of the repository in <directory>

Licence
-------
GNU General Public License, Version 3, 29 June 2007

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License (GPL_) as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.

Automatically generated 23 September 2026.

.. References
.. ..........
.. _background: http://www.ctan.org/pkg/background
.. _ctan: http://www.ctan.org/
.. _git-latexdiff: https://github.com/git-latexdiff/git-latexdiff
.. _latexdiff: http://www.ctan.org/pkg/latexdiff
.. _latexmk: http://www.ctan.org/pkg/latexmk
.. _GPL: http://www.gnu.org/licenses/gpl.html
