file=grants

all:	
	latexmk -pdflatex=lualatex -pdf ${file}.tex && cp ${file}.pdf ../../assets
edit:
	texmaker ${file}.tex &

show:
	evince ${file}.pdf &

clean:
	latexmk -C
