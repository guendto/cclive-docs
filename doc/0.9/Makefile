all:: html

ifndef SHELL_PATH
  SHELL_PATH=/bin/sh
endif
ASCIIDOC ?= asciidoc
A2X ?= a2x
RM ?= rm -f

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

MAN7_TXT=\
  howto-compile-linux.txt

MAN_TXT=$(MAN7_TXT)
MAN_HTML=$(patsubst %.txt,%.html,$(MAN_TXT))

DOC_MAN7=$(patsubst %.txt,%.7,$(MAN7_TXT))
DOC_HTML=$(MAN_HTML)

$(DOC_HTML) $(DOC_MAN7):

$(MAN_HTML): %.html : %.txt
	$(QUIET_ASCIIDOC)$(ASCIIDOC) -d book -b xhtml11 \
		$(ASCIIDOC_OPTS) $*.txt

html: $(DOC_HTML)

$(DOC_MAN7): %.7 : %.txt
	$(QUIET_A2X)$(A2X) -d manpage -f manpage $*.txt

man: man7
man7: $(DOC_MAN7)

clean:
	$(QUIET_CLEAN)$(RM) $(DOC_MAN7) $(DOC_HTML)
