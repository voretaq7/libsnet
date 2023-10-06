# Process this file with autoconf to produce a configure script.
AC_CONFIG_MACRO_DIRS([m4])
AC_INIT([libsnet],[VERSION],[rsug@umich.edu])
AC_CONFIG_HEADERS([config.h])
AC_PREREQ([2.71])
AC_COPYRIGHT([Copyright (c) 1995-2003 Regents of The University of Michigan.  All Rights Reserved.])
AC_CONFIG_SRCDIR([snet.c])

# Checks for programs.
AC_PROG_AWK
AC_PROG_CC
AC_PROG_INSTALL

# Checks for OpenSSL/Crypto
AC_CHECK_HEADER([openssl/ssl.h], [], [AC_MSG_ERROR([header file <openssl/ssl.h> is required.])])
AC_CHECK_LIB([ssl], [SSL_accept], , [AC_MSG_ERROR([Couldn't find SSL_accept in libssl. SSL is mandatory.])])
AC_CHECK_LIB([crypto], [X509_get_subject_name], , [AC_MSG_ERROR([Couldn't find X509_get_subject_name in libcrypto. Crypto support is mandatory.])])

# Checks for zlib.
AC_CHECK_HEADER([zlib.h],
	AC_SEARCH_LIBS([deflate], [z], [AC_DEFINE([HAVE_ZLIB], [1], [zlib.h])], AC_MSG_WARN([Couldn't enable zlib: deflate() not found])),
        AC_MSG_WARN([Couldn't enable zlib: zlib.h not found]))

# Checks for SASL
AC_CHECK_HEADER([sasl/sasl.h],
	AC_SEARCH_LIBS([sasl_client_init], [sasl sasl2 gsasl],
		[AC_DEFINE([HAVE_LIBSASL], [1], [sasl.h])],
		AC_MSG_WARN([Couldn't enable SASL - sasl_client_init() not found]) ),
	AC_MSG_WARN([Couldn't enable SASL - sasl/sasl.h not found]))

AC_CHECK_INCLUDES_DEFAULT
AC_PROG_EGREP

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([gettimeofday select])

# Checks for how to build libraries
AC_DISABLE_SHARED
LT_INIT

# Miscellaneous:
if test x_$GCC = x_yes; then
    OPTOPTS=${OPTOPTS:-"-Wall -Wmissing-prototypes"}
fi
AC_SUBST(OPTOPTS)

# Write output:
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
