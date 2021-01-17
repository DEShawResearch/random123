# This Makefile is EXTREMELY simple.  Let's keep it that way.

all:
	@echo Random123 is a header-only package.  There is nothing to build.
	@echo 'However, "make install" understands prefix, DESTDIR, etc.,'
	@echo 'and "make check" understands CFLAGS, CXXFLAGS, LDFLAGS, etc.'
.PHONY: all

check:
	cd tests && $(MAKE) runcore
.PHONY: check

prefix?=/usr/local
includedir?=$(prefix)/include
datarootdir?=$(prefix)/share
datadir?=$(datarootdir)
docdir?=$(datarootdir)/doc/Random123
export prefix includedir datarootdir datadir docdir

install: install-html install-include install-examples install-tests
.PHONY: install

# recursively copy include/Random123 to $(includedir)
install-include:
	mkdir -p $(DESTDIR)$(includedir)
	cp -dr include/Random123 $(DESTDIR)$(includedir)
.PHONY: install-include

# Run doxygen to install html documentation
install-html:
	mkdir -p $(DESTDIR)$(docdir)
	cd docs; (cat Doxyfile; echo OUTPUT_DIRECTORY=$(DESTDIR)$(docdir)) | doxygen -
.PHONY: install-html

# install-examples and install-tests copy files to
# $(DESTDIR)$(docdir).  Since 'make check' (or other devel activity)
# might "pollute" the examples/ and tests/ directories, the files to
# be copied are enumerated in {examples,tests}/GNUmakefile.
install-examples:
	cd examples; $(MAKE) install
.PHONY: install-examples

install-tests:
	cd tests; $(MAKE) install
.PHONY: install-tests

