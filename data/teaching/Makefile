file=courses

all:	
	latexmk -pdflatex=lualatex -pdf ${file}.tex && cp courses.pdf ../../assets
edit:
	texmaker ${file}.tex &

show:
	evince ${file}.pdf &

clean:
	latexmk -C
