## $Id: Makefile.am,v 1.21 2013/12/31 17:34:00 sebdiaz Exp $

CLEANFILES = *~ stamp

docdir = $(prefix)/doc/$(PACKAGE)-$(VERSION)

FILES = index.tmpl license.tmpl lists.tmpl bugs.tmpl demos.tmpl		\
cgi-overview.tmpl tutorial.tmpl lib-overview.tmpl COPYING COPYING.LIB	\
COPYING.DOC header.html footer.html cgicc-doc.css

IMAGES = $(srcdir)/cgicc.png $(srcdir)/gnu-head-sm.jpg

EXTRA_DIST = html stamp index.tmpl license.tmpl lists.tmpl bugs.tmpl demos.tmpl		\
cgi-overview.tmpl tutorial.tmpl lib-overview.tmpl COPYING COPYING.LIB	\
COPYING.DOC header.html footer.html cgicc-doc.css cgicc.png gnu-head-sm.jpg

SEDCMD1 = s/$$title/GNU cgicc documentation version $(VERSION)/g
SEDCMD2 = s/$$(VERSION)/$(VERSION)/g

all: stamp

clean-local:
	rm -rf html

install-data-local:
	$(mkinstalldirs) $(DESTDIR)@htmldir@
	for file in $(builddir)/html/*; do \
		bn="`basename $$file`"; \
	 	$(INSTALL_DATA) $$file $(DESTDIR)@htmldir@/$$bn; \
	done

uninstall-local:
	for file in $(srcdir)/html/*; do \
		bn="`basename $$file`"; \
		rm -f $(DESTDIR)@htmldir@/$$bn; \
	done

## Dummy rule to build a timestamp file
stamp: Doxyfile $(FILES) $(top_srcdir)/cgicc/*.h $(top_srcdir)/demo/*.cpp
	$(MAKE) html-doc
	touch $@

## Generate documentation
html-doc:
	if test ! -d $(builddir)/html; then \
		mkdir $(builddir)/html; \
	fi;
	DATE=`date '+%-d %b %Y'` VERSION=$(VERSION) $(DOXYGEN) Doxyfile
	cp $(IMAGES) $(srcdir)/cgicc-doc.css $(builddir)/html
	if test ! -d $(builddir)/html/index.html; then \
		echo empty> $(builddir)/html/index.html; \
	fi;
	mv $(builddir)/html/index.html $(builddir)/html/index.html.bak
	sed -e '$(SEDCMD1)' -e '$(SEDCMD2)' $(builddir)/html/index.html.bak > $(builddir)/html/index.html
	rm -f $(builddir)/html/index.html.bak
