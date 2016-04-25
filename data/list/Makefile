file=list

all:	
	latexmk -pdf ${file}.tex
edit:
	texmaker ${file}.tex &

show:
	evince ${file}.pdf &

clean:
	latexmk -C
