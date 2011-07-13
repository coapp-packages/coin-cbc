# Copyright (C) 2006 International Business Machines and others.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

## $Id: Makefile.am 198 2011-01-01 14:09:13Z stefan $

# Author:  Andreas Waechter           IBM    2006-04-13

AUTOMAKE_OPTIONS = foreign

########################################################################
#                List files that should be distributed                 #
########################################################################

EXTRA_DIST = $(EXAMPLE_FILES) README AUTHORS LICENSE

DISTCLEANFILES = $(EXAMPLE_CLEAN_FILES)

datacoindir = $(datadir)/coin/Data/Sample
datacoin_DATA = $(EXAMPLE_FILES)

coindocdir = $(datadir)/coin/doc/Data/Sample
coindoc_DATA = README AUTHORS LICENSE

pkgconfiglibdir = $(libdir)/pkgconfig
pkgconfiglib_DATA = coindatasample.pc

include BuildTools/Makemain.inc
