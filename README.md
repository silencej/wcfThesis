wcfThesis
=========

LaTeX thesis template for CAS.

Because the abstract needs to write in chinese, so xelatex is chosen instead of pdftex.
Because there are often non-ascii chars in bibliography files, biber is chosen instead of oldschool bitex.

Put all images (PDF is better, png .etc are also OK) under images directory.
Modify your bib reference in refs/all.bib.
Directory "en" is for storing enlish version.

Usage:
cd en
make full

"Make full" will automatically do xelatex 3 times plus biber once, and remind you when all jobs are done by ringing a bell (command vlc must be installed or you'd hope "echo ^G" would work under MS-DOS windows). Simply type "make" will run xelatex once.
"make touch" will remove the main.pdf for you so you could use "make full" again.
Modify Makefile on demands of your own.

The "doorbell.mp3" is public domain copyrighted.

