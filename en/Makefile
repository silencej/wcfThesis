# -*- mode:makefile; -*-

# Specify your variables here.

targets:=main.pdf
# forceTarg:=pollenSymp
tempDir:=../wcfThesis
allBib:=../refs/all.bib
tempFile:=wcfThesis.sty
makeGlossFlag:=1
globals:=${wildcard chapter/*.tex}

#=====================================================#
# Display Codes (this is so we can track passes)
#=====================================================#
MOVE_TO_COL	= @echo -en "\\033[60G"
SETCOLOR_BLACK	= @echo -en "\\033[0;30m"
SETCOLOR_RED 	= @echo -en "\\033[0;31m"
SETCOLOR_GREEN 	= @echo -en "\\033[0;32m"
SETCOLOR_BLUE	= @echo -en "\\033[0;34m"

fullFlag:=0

texDir = .
texs:=$(wildcard $(texDir)/*.tex)
bibs:=${allBib}
# pdfs:=$(texs:.tex=.pdf)
pdfs:=${targets}
globals+=${tempDir}/${tempFile} ${bibs} ${texs}
# ${globalsOther}

# If using refsections, you need to run bibtex on all *[1-9]-blx.aux.
# Must be protected by quotes for xargs.
# biblatexAux:="enMain1-blx enMain2-blx"

#LATEX = pdflatex
LATEX = xelatex
LATEX_FLAGS =
BIBTEX = biber
BIB_FLAGS =

#=====================================================#
# Standard Targets                                    #
#=====================================================#
.phony : all clean touch clean-all full force once

## Make only once for all texs. Only changed texs will be made.
all once full: ${targets}
#	${LATEX} ${LATEX_FLAGS} $?

# ${pdfs}: %.pdf : %.tex ${globals}
# 	$(LATEX) $(LATEX_FLAGS) $(*F)

# Set target-specific variable.
# full: fullFlag:=1
# Use:
# make fullFlag=1
# full: ${targets}

#%.pdf : %.tex %.aux %.bbl
# The pattern rules could only specify 1 pre-requisite, or it will lose effect.
${pdfs}: %.pdf : %.tex ${globals}
#ifneq (1,${fullFlag})
ifneq (${MAKECMDGOALS},full)
	$(LATEX) $(LATEX_FLAGS) $(*F)
else
	-make clean
	$(LATEX) $(LATEX_FLAGS) $(*F)
	${BIBTEX} $(*F)
#	ls *blx.aux | xargs -L 1 bibtex
#	makeglossaries ${*F}
	$(if $(findstring makeGlossFlag,1), makeglossaries ${*F})
#	-makeindex $(*F)
#	-makeindex enMain.nlo -s nomencl.ist -o enMain.nls
	$(LATEX) $(LATEX_FLAGS) $(*F)
	$(LATEX) $(LATEX_FLAGS) $(*F)
# Make beep when finished. @: disabling recipe echoing.
	@-echo 
# In linux?
	@-cvlc --no-loop --no-repeat --play-and-exit -q ${tempDir}/doorBell-SoundBible.com-1986366504.mp3
#	-echo -en "\007"
	@echo "Full latexing finished."
endif

clean:
	-rm $(targets) *.aux *.bbl

touch :
	-rm $(targets)
#	-rm enMain.pdf *.bbl *.aux *.blg enMain.idx enMain.ilg enMain.lof enMain.lot enMain.toc enMain-blx.bib enMain.out enMain.ind enMain.run.xml enMain.nl?

clean-all :
	rm -f *.aux *.bbl *.blg *.log *.lof *.lot *.out *.toc *.pdf chapter/*.aux

# Will always compile without prerequisites.
force:
	$(LATEX) $(LATEX_FLAGS) ${forceTarg}
	${BIBTEX} ${forceTarg}
	ls *blx.aux | xargs -L 1 ${BIBTEX}
	$(LATEX) $(LATEX_FLAGS) ${forceTarg}
	$(LATEX) $(LATEX_FLAGS) ${forceTarg}

# To generate a .pdf file from a .tex file
# %.bib must be the first prerequisite.
# %.pdf : %.bib %.tex
# 	$(LATEX) $(LATEX_FLAGS) $(*F)
# # ifeq "$(findstring $(<),$(wildcard *.bib))" ""
# #	bibtex $(*F)
# 	bibtex $(*F)
# 	$(LATEX) $(LATEX_FLAGS) $(*F)
# 	$(LATEX) $(LATEX_FLAGS) $(*F)
# # endif

# %.aux : %.tex
# 	pdflatex $(*F)
# 
# %.bbl : main.bib %.aux %.tex
# 	bibtex $(*F)

