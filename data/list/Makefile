file=list

all:	
	pdflatex ${file}.tex
	bibtex talk 
	bibtex book	
	pdflatex ${file}.tex
	pdflatex ${file}.tex
edit:
	texmaker ${file}.tex &

show:
	evince ${file}.pdf &

