# Copyright (C) 2006 International Business Machines and others.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

## $Id: Makefile.am 1675 2011-06-19 17:23:14Z stefan $

# Author:  Andreas Waechter           IBM    2006-04-13

AUTOMAKE_OPTIONS = foreign

########################################################################
#                         unitTest for Cbc                             #
########################################################################

CBC_TEST_TGTS = gamstests ositests

if COIN_HAS_CLP
  CBC_TEST_TGTS += test_cbc
endif
if CBC_BUILD_CBC_GENERIC
if COIN_HAS_SAMPLE
  CBC_TEST_TGTS += test_cbc_generic
endif
endif

cbcflags =
ositestsflags =
if COIN_HAS_SAMPLE
  cbcflags += -dirSample `$(CYGPATH_W) $(SAMPLE_DATA)`
  ositestsflags += -mpsDir=`$(CYGPATH_W) $(SAMPLE_DATA)`
endif
cbcflags += -unitTest
if COIN_HAS_MIPLIB3
  cbcflags += -dirMiplib `$(CYGPATH_W) $(MIPLIB3_DATA)` -miplib
endif
if COIN_HAS_NETLIB
  ositestsflags += -netlibDir=`$(CYGPATH_W) $(NETLIB_DATA)` -testOsiSolverInterface
endif

# We are using the solver executables to do the unit test

test: $(CBC_TEST_TGTS)

test_cbc: ../src/cbc$(EXEEXT)
	../src/cbc$(EXEEXT) $(cbcflags)

if COIN_HAS_SAMPLE
test_cbc_generic: ../src/cbc-generic$(EXEEXT)
	echo "A minimal test is all that cbc-generic can manage just yet."
	../src/cbc-generic$(EXEEXT) \
	    -directory `$(CYGPATH_W) $(SAMPLE_DATA)` -import p0033.mps -branch
endif

gamstests: gamsTest$(EXEEXT)
	./gamsTest$(EXEEXT)

.PHONY: test

bin_PROGRAMS = gamsTest osiUnitTest

gamsTest_SOURCES = gamsTest.cpp
gamsTest_LDADD = ../src/libCbcSolver.la ../src/libCbc.la $(CBCLIB_LIBS)
gamsTest_DEPENDENCIES = ../src/libCbcSolver.la ../src/libCbc.la $(CBCLIB_DEPENDENCIES)

AM_CPPFLAGS = -I`$(CYGPATH_W) $(srcdir)/../src` $(COINDEPEND_CFLAGS)
AM_CPPFLAGS += $(CLP_CFLAGS) $(CPX_CFLAGS) $(DYLP_CFLAGS) $(GLPK_CFLAGS) $(MSK_CFLAGS) $(VOL_CFLAGS) $(XPR_CFLAGS)

# This line is necessary to allow VPATH compilation
DEFAULT_INCLUDES = -I. -I`$(CYGPATH_W) $(srcdir)` -I$(top_builddir)/src

########################################################################
#                         unitTest for OsiCbc                          #
########################################################################

osiUnitTest_SOURCES = osiUnitTest.cpp OsiCbcSolverInterfaceTest.cpp

osiUnitTest_LDADD = ../src/OsiCbc/libOsiCbc.la ../src/libCbc.la \
    $(CBCLIB_LIBS) $(OSITESTS_LIBS)

osiUnitTest_DEPENDENCIES = ../src/OsiCbc/libOsiCbc.la ../src/libCbc.la \
    $(CBCLIB_DEPENDENCIES) $(OSITESTS_DEPENDENCIES)

AM_CPPFLAGS += $(OSITESTS_CFLAGS) \
        -I`$(CYGPATH_W) $(srcdir)/../src/OsiCbc`

ositests: osiUnitTest$(EXEEXT)
	./osiUnitTest$(EXEEXT) $(ositestsflags)

########################################################################
#                          Cleaning stuff                              #
########################################################################

# Here we list everything that is not generated by the compiler, e.g.,
# output files of a program

DISTCLEANFILES = yy.mps xx.mps continuous.mps integer.mps test2.lp test2.out test.lp test.mps test.out x1.mps.mps x2.mps.mps x3.mps.mps
