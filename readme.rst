======================
git-lpdf and git-ldiff
======================
A bash script for producing pdf files from a git repository that tracks latex
documents. There are two modes:
 - lpdf:  produces a latex file for the given commit in the repository
 - ldiff: uses latexdiff to create a pdf file that highlights the differences between commits
This script is partially motivated by the script git-latexdiff_ and my
attempts to get it to work the way that I wanted. The date and commit information is printed 
as a banner on the PDF files. This script should be used from inside git.
  
The main idea of the script is to provide an easy way to produce a PDF file
from a git repository that is clearly annotated with the commit data. For
example:
.. code:: bash
   > git lpdf <commit>
will produce a PDF file for the commit <commit> of the latex file in the current
repository. Using latexdiff_, the command
.. code:: bash
   > git ldiff <commit>
produces a PDF file that highlights the differences between the commit <commit> and the current
working copy of the latex file in the current repository. Similarly,
.. code:: bash
   > git ldiff <commit1> <commit1>
produces a PDf file showing he differences between two commits.
  
In all cases the commit information is printed on all pages of the PDF.
  
Andrew Mathas June 2014
  
Installation
============
  
Clone the git repository, or download the shell script, and then type:
  ./git-ldiff --install [directory]   # directory defaults to /Users/andrew/bin
This will create two links, git-lpdf and git-ldiff, in the specified directory
to the shell script git-ldiff. This directory should be in your path.
  
The script makes use of the backgrounds_ package andlatexdiff_. Both of these
are available from ctan and are automatically installed with TeXLive.
.. code:: bash
.. code:: bash
.. code:: bash

Usage for lpdf script
=====================
Usage: git lpdf [--main file] [--latex latex executable] [commit]

Creates a PDF file for the main latex file in the repository with commit
information printed as a banner down the left hand margin on each page.

Examples:
## .. code:: bash
  > git lpdf           # produces time-stamped "Latest version" of main latex file
  > git lpdf b675cdf   # produces pdf file for main latex file as of commit b675cdf
  > git lpdf --main myfile.tex # produces pdf file for my file as of commit b675cdf

By default the script uses pdflatex. This can be changed using the --latex option:
## .. code:: bash
  > git lpdf --latex   # produces time-stamped "Latest version" of main latex file

Usage for ldiff script
======================
Usage: git ldiff [--main file] [--latex latex executable] [OLD] [NEW]

To use this mode you need to have latexdiff_ installed.

By default the files in the HEAD of the git repository are compared with
the files in current working directory. Ostensibly, OLD and NEW are git shas
in the current repository, however, we also allow them to be --, for the files
in the current working directory, or another directory.

Examples:
## .. code:: bash
  > git ldiff   # compare most recent commit with current (uncommited) version
  > git ldiff --main myfile.tex  # compare most recent commit for myfile  with current version
  > git ldiff <commit> # compare commit with current verion
  > git ldiff <dirame> [commit] # compare version in directory <dirname> with specified commit

 There are also --safe and --verysafe options that are sometimes more
 successful in getting latexdiff to work.
    

To do
=====
 - better handling of latexdiff options
 - clean up the argument parsing
 - improve documentation 

Licence
=======
GNU General Public License, Version 3, 29 June 2007

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License (GPL_) as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.


.. References
.. _background: http://www.ctan.org/pkg/background
.. _git-latexdiff: https://gitorious.org/git-latexdiff
.. _latexdiff: http://www.ctan.org/pkg/latexdiff
.. _GPL: http://www.gnu.org/licenses/gpl.html

.. Automatically generated Mon 24 Nov 2014 23:36:44 AEDT.
