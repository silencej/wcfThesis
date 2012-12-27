wcfThesis
=========

LaTeX thesis template for CAS.

Because the abstract needs to write in chinese, so xelatex is chosen instead of pdftex.
Because there are often non-ascii chars in bibliography files, biber is chosen instead of oldschool bitex.

Usage:
cd en
make full

Directory "en" is for storing enlish version. "Make full" will automatically do xelatex 3 times plus biber once. Simply type "make" will run xelatex once.
"make touch" will remove the main.pdf for you so you could use "make full" again.
Modify Makefile on demands of your own.

The "doorbell.mp3" is public domain copyrighted.
