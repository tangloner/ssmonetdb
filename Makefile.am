-include Makefile.local

BUILT_SOURCES = gitrev.h
CLEANFILES = gitrev.h

bin_PROGRAMS = sqlsmith

DUT = postgres.cc monetdb.cc

if DUT_SQLITE
DUT += sqlite.cc
endif


sqlsmith_SOURCES = relmodel.cc schema.cc $(DUT)	 			\
    random.cc prod.cc expr.cc grammar.cc log.cc dump.cc impedance.cc	\
    sqlsmith.cc

sqlsmith_LDADD = $(LIBPQXX_LIBS) $(MONETDB_MAPI_LIBS) $(BOOST_REGEX_LIB) -lpq

AM_LDFLAGS = $(BOOST_LDFLAGS)
AM_CPPFLAGS = $(BOOST_CPPFLAGS) $(LIBPQXX_CFLAGS) $(MONETDB_MAPI_CFLAGS)  -Wall -Wextra


EXTRA_DIST = gitrev.h dump.hh expr.hh grammar.hh log.hh prod.hh		\
    random.hh relmodel.hh schema.hh impedance.hh filter.sql log.sql	\
    README.org TODO.org ast.png logo.png dump.xsl util.hh sqlite.hh	\
    dut.hh postgres.hh monetdb.hh log-v1.0-to-v1.1.sql

gitrev.h: $(HEADERS) $(SOURCES)
	echo "#define GITREV \"$$(git describe --dirty --tags --always)\"" > $@

filterdump:
	psql -c 'copy (select error from known) to stdout' smith|sort -u > known.txt
	psql -c 'copy (select re from known_re) to stdout' smith|sort -u > known_re.txt

.PHONY: filterdump
