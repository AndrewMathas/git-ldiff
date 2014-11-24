A bash script for producing pdf files from a git repository that tracks latex
documents. There are two modes:
 - ldiff: uses latexdiff to create a pdf file that highlights the differences between commits
 - lpdf:  produces a latex file for the given commit in the repository
script is partially based on the git-latexdiff script available on the web.
The date and commit information are printed as a banner on the PDF files.

Andrew Mathas June 2014

TODO
 - clean up the argument parsing
 - better handling of latexdiff options
 - improve documentation 

INSTALLATION

Clone the git repository, or download the shell script, and then type:
  ./git-ldiff --install [directory]   # directory defaults to /Users/andrew/bin
This will create two links, git-lpdf and git-ldiff, in the specified directory
to the shell script git-ldiff. This directory should be in your path
  grep "" $0 | sed 's/## //' > $readme

USAGE FOR LPDF SCRIPT
Usage: git lpdf [--main file] [--latex latex executable] [commit]

Creates a PDF file for the main latex file in the repository with commit
information printed as a banner down the left hand margin on each page.

  Examples:
    > git lpdf           # produces time-stamped "Latest version" of main latex file
    > git lpdf b675cdf   # produces pdf file for main latex file as of commit b675cdf
    > git lpdf --main myfile.tex # produces pdf file for my file as of commit b675cdf

  By default the script uses pdflatex. This can be changed using the --latex option:
    > git lpdf --latex   # produces time-stamped "Latest version" of main latex file

USAGE FOR LDIFF SCRIPT
Usage: git ldiff [--main file] [--latex latex executable] [OLD] [NEW]

This mode requires latexdiff <http:...>

By default the files in the HEAD of the git repository are compared with
the files in current working directory. Ostensibly, OLD and NEW are git shas
in the current repository, however, we also allow them to be --, for the files
in the current working directory, or another directory.

  Examples:
