# Copyright (C) 2006 International Business Machines and others.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

## $Id: Makefile.am 1033 2011-06-19 16:49:13Z stefan $

# Author:  Andreas Waechter           IBM    2006-04-13

AUTOMAKE_OPTIONS = foreign

########################################################################
#                          Subdirectories                              #
########################################################################

SUBDIRS = src

# We don't want to compile the test subdirectory, unless the test target is
# specified.  But we need to list it as subdirectory to make sure that it is
# included in the tarball

if ALWAYS_FALSE
  SUBDIRS += test
endif

########################################################################
#             Additional files to be included in tarball               #
########################################################################

# Here we need include all files that are not mentioned in other Makefiles

EXTRA_DIST = examples/cgl1.cpp \
	examples/cgl_data_test.cpp \
	examples/Makefile.in

########################################################################
#                           Extra Targets                              #
########################################################################

test: all
	cd test; $(MAKE) test

unitTest: test

# Doxygen documentation

doxydoc:
	doxygen doxydoc/doxygen.conf

clean-doxydoc:
	( cd doxydoc ; rm -rf html *.log *.tag )


clean-local: clean-doxydoc
	if test -r test/Makefile; then cd test; $(MAKE) clean; fi

distclean-local:
	if test -r test/Makefile; then cd test; $(MAKE) distclean; fi

install-exec-local: install-doc

uninstall-local: uninstall-doc

.PHONY: test unitTest doxydoc

########################################################################
#                  Installation of the addlibs file                    #
########################################################################

pkgconfiglibdir = $(libdir)/pkgconfig
pkgconfiglib_DATA = cgl.pc

addlibsdir = $(DESTDIR)$(datadir)/coin/doc/Cgl
	
install-data-hook:
	@$(mkdir_p) "$(addlibsdir)"
if COIN_HAS_PKGCONFIG
	PKG_CONFIG_PATH=@COIN_PKG_CONFIG_PATH@ \
	$(PKG_CONFIG) --libs cgl > $(addlibsdir)/cgl_addlibs.txt
else
if COIN_CXX_IS_CL
	echo "/libpath:`$(CYGPATH_W) @abs_lib_dir@` libCgl.lib @CGLLIB_LIBS_INSTALLED@" > $(addlibsdir)/cgl_addlibs_cpp.txt
else
	echo -L@abs_lib_dir@ -lCgl @CGLLIB_LIBS_INSTALLED@ > $(addlibsdir)/cgl_addlibs.txt
endif
endif

uninstall-hook:
	rm -f $(addlibsdir)/cgl_addlibs.txt

########################################################################
#                         Maintainer Stuff                             #
########################################################################

CLEANFILES =

# Files that are generated and should be cleaned with make distclean
DISTCLEANFILES =

include BuildTools/Makemain.inc
