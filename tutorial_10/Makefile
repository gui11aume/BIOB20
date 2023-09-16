DOC:= BIOB20_tutorial_10.Snw

RERUN:= "(undefined references|Rerun to get (cross-references|the bars|point totals) right|Table widths have changed. Rerun LaTeX.|Linenumber reference failed)"
RERUNBIB:= "No file.*\.bbl|Citation.*undefined"

all: doc

doc: $(DOC:.Snw=.pdf)

%.tex: %.Snw
	R CMD Sweave $<

%.pdf: %.tex
	TEXINPUTS=".;../sty;$$TEXINPUTS" pdflatex $<
	@egrep -q $(RERUNBIB) $*.log && bibtex $* && TEXINPUTS=".;../sty;$$TEXINPUTS" pdflatex $<; true
	@egrep -q $(RERUN) $*.log && TEXINPUTS=".;../sty;$$TEXINPUTS" pdflatex $<; true
	@egrep -q $(RERUN) $*.log && TEXINPUTS=".;../sty;$$TEXINPUTS" pdflatex $<; true

latexmk: $(DOC:.Snw=.tex)
	-latexmk -pvc -pdf $<

purge:
	-rm -f *.{aux,dvi,log,bbl,blg,brf,fls,toc,thm,out,fdb_latexmk}

clean: purge
	-rm -f $(DOC:.Snw=.pdf) $(DOC:.Snw=.tex)

.PHONY: all purge clean
