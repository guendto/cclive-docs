all:: html

ifndef SHELL_PATH
  SHELL_PATH=/bin/sh
endif
ASCIIDOC ?= asciidoc
A2X ?= a2x
RM ?= rm -f

# Options
PDF_FOOP ?= --fop # undefine to force dblatex

ifndef V
  QUIET_ASCIIDOC=@echo '   ' ASCIIDOC $@;
  QUIET_CLEAN=@echo '   ' CLEAN;
  QUIET_A2X=@echo '   ' A2X $@;
endif

ASCIIDOC_OPTS=\
  -a disable-javascript\
  -a stylesdir=style\
  -a max-width=70em\
  -a linkcss\
  -a icons

PAGE_TXT=\
  mailinglist.txt\
  faq_general.txt\
  contrib.txt\
  index.txt

DOC_HTML=$(patsubst %.txt,%.html,$(PAGE_TXT))
DOC_PDF=$(patsubst %.txt,%.pdf,$(PAGE_TXT))

$(DOC_HTML): %.html : %.txt
	$(QUIET_ASCIIDOC)$(ASCIIDOC) -d book -b xhtml11 \
		$(ASCIIDOC_OPTS) $*.txt

$(DOC_PDF): %.pdf : %.txt
	$(QUIET_A2X)$(A2X) -d book -f pdf $(PDF_FOOP) \
		--asciidoc-opts="$(ASCIIDOC_OPTS)" $*.txt

html: $(DOC_HTML)
pdf: $(DOC_PDF)

clean:
	$(QUIET_CLEAN)$(RM) $(DOC_HTML) $(DOC_PDF)

