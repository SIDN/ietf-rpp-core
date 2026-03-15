MMARK :=mmark
TXT := $(patsubst %.md,%.txt,$(wildcard *.md))
NOPAGINATION_TXT := $(patsubst %.md,%.clean.txt,$(wildcard *.md))
XML := $(patsubst %.md,%.xml,$(wildcard *.md))
HTML := $(patsubst %.md,%.html,$(wildcard *.md))
PDF := $(patsubst %.md,%.pdf,$(wildcard *.md))



txt: $(TXT)

%.txt: %.xml
	xml2rfc --text --v3 ../docs/$< -p ../docs --list-symbols -


nopagination-txt: $(NOPAGINATION_TXT)

%.clean.txt: %.xml
	xml2rfc -P --text --v3 ../docs/$< --out  ../docs/$@ --list-symbols -
	$(if $(filter nopagination-txt,$(MAKECMDGOALS)),git checkout -- ../docs/$<)


html: $(HTML)

%.html: %.xml
	xml2rfc --html --v3 ../docs/$< -p ../docs 

xml: $(XML)

%.xml: %.md
	$(MMARK) $< > ../docs/$(basename $<).xml

pdf: $(PDF)

%.pdf: %.xml
	xml2rfc --pdf --v3 ../docs/$< -p ../docs

.PHONY: clean
clean:
	rm -f *.txt *.xml

all: txt html pdf nopagination-txt