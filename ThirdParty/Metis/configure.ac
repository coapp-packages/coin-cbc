# Copyright (C) 2009 International Business Machines.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

## $Id: configure.ac 2015 2010-12-26 16:11:54Z stefan $

# Author:  Andreas Waechter            IBM    2009-04-20

#############################################################################
#                       Names and other basic things                        #
#############################################################################

AC_PREREQ(2.59)

AC_INIT([ThirdPartyMetis],[1.2],[http://projects.coin-or.org/BuildTools/newticket])

AC_COPYRIGHT([
Copyright 2009 International Business Machines and others.
All Rights Reserved.
This file is part of the open source package Coin which is distributed
under the Eclipse Public License.])

# List one file in the package so that the configure script can test
# whether the package is actually there
AC_CONFIG_SRCDIR(metis-4.0/Lib/balance.c)

# Where should everything be installed by default?  Here, we want it
# to be installed directly in 'bin', 'lib', 'include' subdirectories
# of the directory where configure is run.  The default would be
# /usr/local.
AC_PREFIX_DEFAULT([`pwd`])

AC_COIN_PROJECTDIR_INIT(Metis)

#############################################################################
#                         Standard build tool stuff                         #
#############################################################################

# Get the system type
AC_CANONICAL_BUILD

#turn off warnings and pedantic mode since they could make trouble on some platforms,
#and we couldn't fix them anyway
coin_skip_warn_cflags=yes
coin_skip_warn_fflags=yes

# Check if user wants to produce debugging code
AC_COIN_DEBUG_COMPILE(Metis)

# Get the name of the C compiler
AC_COIN_PROG_CC

# Check if pkg-config is available (to setup addlibs file)
AC_COIN_HAS_PKGCONFIG

# Initialize automake
AC_COIN_INIT_AUTO_TOOLS

# We need to create a dummy header file for Windows
AC_MSG_CHECKING([whether we need to create a dummy strings.h file])
if test "$ac_cv_header_strings_h" = no; then
  AC_MSG_RESULT([yes])
  touch strings.h
else
  AC_MSG_RESULT([no])
fi

# On some systems, there are no drand48 and srand48.
# By defining __VC__, we can make Metis use an alternative function
AC_CHECK_FUNC(drand48,,[CFLAGS="$CFLAGS -D__VC__"])

METISDIR=metis-4.0
AC_SUBST(METISDIR)

AC_CONFIG_FILES([Makefile coinmetis.pc coinmetis-uninstalled.pc])

AC_COIN_FINALIZE
