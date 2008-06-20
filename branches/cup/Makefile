py	LATEX = latex

DVIPS = dvips

PDFFLAGS = -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress \
           -dCompressPages=true -dUseFlateCompression=true  \
           -dEmbedAllFonts=true -dSubsetFonts=true -dMaxSubsetPct=100


%.dvi: %.tex
	$(LATEX) $<

%.ps: %.dvi
	$(DVIPS) -o $@ $<

%.pdf: %.ps
	ps2pdf $(PDFFLAGS) $<

all:	book.tex
	latex book
	makeindex book
	latex book
#	dvips -T 6.75in,9.25in -Ppdf -o thinkpython.ps book
#	dvips -t letter -Ppdf -o thinkpython.ps book
#	dvips -t b5 -Ppdf -o thinkpython.ps book
	dvips -T 7in,10in -Ppdf -o thinkpython.ps book
	gv thinkpython.ps


DEST = /home/downey/public_html/cup

distrib:
	ps2pdf $(PDFFLAGS) thinkpython.ps
	rm -rf dist
	mkdir dist dist/tex dist/tex/figs
	rsync -a thinkpython.pdf dist
	rsync -a Makefile book.tex cupbook.cls dist/tex
	rsync -a figs/*.fig figs/*.eps dist/tex/figs
	cd dist; zip -r thinkpython.tex.zip tex
	rsync -a dist/* $(DEST)
	chmod -R o+r $(DEST)/*

clean:
	rm -f *~ *.aux *.log *.dvi *.idx *.ilg *.ind *.toc



