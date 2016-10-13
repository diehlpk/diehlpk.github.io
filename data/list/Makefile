file=list

all:	
	latexmk -pdf ${file}.tex && cp list.pdf ../../assets
edit:
	texmaker ${file}.tex &

show:
	evince ${file}.pdf &

clean:
	latexmk -C
