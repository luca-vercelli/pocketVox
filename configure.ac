m4_define([pocketvox_major], [0])
m4_define([pocketvox_minor], [0])

#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
# ATTENTION version IMPAIRES pour les devs
# et PAIRS pour les releases
m4_define([pocketvox_micro], [1])
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

m4_define([pocketvox_version],
        [pocketvox_major.pocketvox_minor.pocketvox_micro])

# autoconf
AC_INIT([pocketvox],[pocketvox_version])
AC_CONFIG_MACRO_DIR([build/autotools])

AM_INIT_AUTOMAKE
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

# Check local libtool
AC_PROG_LIBTOOL

# Handle cross-compil mode
AC_CANONICAL_HOST

AM_MAINTAINER_MODE

AC_CONFIG_HEADERS([config.h])

AC_ISC_POSIX
AC_HEADER_STDC
AC_DISABLE_STATIC
AC_PROG_LIBTOOL
AM_PROG_CC_C_O
AC_PROG_CXX
AM_PATH_GLIB_2_0
PKG_PROG_PKG_CONFIG([0.16])

POCKETVOX_MAJOR_VERSION=pocketvox_major
POCKETVOX_MINOR_VERSION=pocketvox_minor
POCKETVOX_MICRO_VERSION=pocketvox_micro
POCKETVOX_VERSION=pocketvox_version
AC_SUBST(POCKETVOX_MAJOR_VERSION)
AC_SUBST(POCKETVOX_MINOR_VERSION)
AC_SUBST(POCKETVOX_MICRO_VERSION)
AC_SUBST(POCKETVOX_VERSION)

AC_DEFINE_UNQUOTED(POCKETVOX_PREFIX, "${prefix}", [prefix])
PREFIX=${prefix}
AC_SUBST(PREFIX)

LT_PREREQ([2.2.6])
LT_INIT([disable-static])


dnl
dnl View options
dnl
AC_ARG_ENABLE([debug],
    AS_HELP_STRING([--enable-debug],[Set debug CFLAGS]),,
    enable_debug=$profile_enable_debug)

dnl
dnl Enable debug
dnl
AC_MSG_CHECKING(for debug flags)
if test "x$enable_debug" = "xyes"; then
    DEBUG_CFLAGS="-O0 -g3 -fno-strict-aliasing"
    dnl -finstrument-functions"
    AC_DEFINE(ENABLE_DEBUG, 1, [Debug CFLAGS on])
    AC_MSG_RESULT(debug on)
else
    DEBUG_CFLAGS="-fno-strict-aliasing"
    AC_MSG_RESULT(debug off)
fi

dnl
dnl Check Deps  
dnl 

PKG_CONFIG_PATH+=":/usr/local/lib/pkgconfig:/usr/lib/i386-linux-gnu/pkgconfig"

PKG_CHECK_MODULES(GLIB, [glib-2.0])
AC_MSG_RESULT([GLIB_CFLAGS=$GLIB_CFLAGS])
AC_MSG_RESULT([GLIB_LIBS=$GLIB_LIBS])

AC_SUBST(GLIB_CFLAGS)
AC_SUBST(GLIB_LIBS)

PKG_CHECK_MODULES(GSTREAMER, [gstreamer-0.10])
AC_MSG_RESULT([GSTREAMER_CFLAGS=$GSTREAMER_CFLAGS])
AC_MSG_RESULT([GSTREAMER_LIBS=$GSTREAMER_LIBS])

AC_SUBST(GSTREAMER_CFLAGS)
AC_SUBST(GSTREAMER_LIBS)

PKG_CHECK_MODULES(GTK3, [gtk+-3.0])
AC_MSG_RESULT([GTK3_CFLAGS=$GTK3_CFLAGS])
AC_MSG_RESULT([GTK3_LIBS=$GTK3_LIBS])

AC_SUBST(GTK3_CFLAGS)
AC_SUBST(GTK3_LIBS)

PKG_CHECK_MODULES(POCKETSPHINX, [pocketsphinx])
AC_MSG_RESULT([POCKETSPHINX_CFLAGS=$POCKETSPHINX_CFLAGS])
AC_MSG_RESULT([POCKETSPHINX_LIBS=$POCKETSPHINX_LIBS])

AC_SUBST(POCKETSPHINX_CFLAGS)
AC_SUBST(POCKETSPHINX_LIBS)

PKG_CHECK_MODULES(LIBNOTIFY, [libnotify])
AC_MSG_RESULT([LIBNOTIFY_CFLAGS=$LIBNOTIFY_CFLAGS])
AC_MSG_RESULT([LIBNOTIFY_LIBS=$LIBNOTIFY_LIBS])

AC_SUBST(LIBNOTIFY_CFLAGS)
AC_SUBST(LIBNOTIFY_LIBS)

PKG_CHECK_MODULES(APPINDICATOR, [appindicator3-0.1])
AC_MSG_RESULT([APPINDICATOR_CFLAGS=$APPINDICATOR_CFLAGS])
AC_MSG_RESULT([APPINDICATOR_LIBS=$APPINDICATOR_LIBS])

AC_SUBST(APPINDICATOR_CFLAGS)
AC_SUBST(APPINDICATOR_LIBS)


dnl
dnl Add Extra CFLAGS
dnl
WARNING_CFLAGS=" -Wall  -Werror  -Wshadow \
                -Wno-uninitialized -Wno-strict-aliasing \
                -Wformat -Wformat-security \
                -Winit-self  -Wpointer-arith"

DEBUG_CFLAGS+=$WARNING_CFLAGS

dnl
dnl Finely set DEBUG_CFLAGS
dnl
AC_SUBST(DEBUG_CFLAGS)


AC_CONFIG_FILES([
                Makefile
                src/Makefile
                pocketvox.pc
])

AC_OUTPUT