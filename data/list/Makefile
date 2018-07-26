file=list

all:	
	latexmk -pdflatex=lualatex -pdf ${file}.tex && cp list.pdf ../../assets
edit:
	texmaker ${file}.tex &

show:
	evince ${file}.pdf &

clean:
	latexmk -C
