long:
	latexmk -pdf long.tex &&  cp long.pdf ../../assets/cv.pdf

short:
	latexmk -pdf short.tex

clean:
	latexmk -C

showLong:
	evince long.pdf &

showShort:
	evince short.pdf &
