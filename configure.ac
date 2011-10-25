AC_PREREQ(2.53)
AC_INIT(meego-panel-zones, 0.3.0)
AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)
AC_CONFIG_MACRO_DIR([m4])
AM_CONFIG_HEADER(config.h)

AC_CANONICAL_HOST
AS_ALL_LINGUAS
IT_PROG_INTLTOOL([0.35.0])

GETTEXT_PACKAGE=meego-panel-zones
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE],
                   ["$GETTEXT_PACKAGE"],
                   [Gettext domain name])
AM_GLIB_GNU_GETTEXT

AC_PROG_CC
AC_PROG_CC_STDC
AC_PROG_INSTALL
AC_PROG_LIBTOOL
AC_ISC_POSIX
AC_HEADER_STDC
AM_PROG_CC_C_O

# enable quiet ("silent") builds, if available
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])



CFLAGS="$CFLAGS -Wall -Wextra -Wno-unused-parameter -Wno-missing-field-initializers"

PKG_CHECK_MODULES(MPL, meego-panel >= 0.50.0)

MEEGO_PANELS_DIR=`$PKG_CONFIG --variable=meego_panel_panels_dir meego-panel`
AC_SUBST(MEEGO_PANELS_DIR)

PKG_CHECK_MODULES(ZONES,
                  clutter-gtk-0.12
                  gtk+-2.0 >= 2.14
                  mx-1.0
                  libwnck-1.0
                  gconf-2.0
                  )

AC_ARG_ENABLE([cache],
              [AC_HELP_STRING([--enable-cache],
                              [Enable Nbtk image cache generation])],
              [],
              [enable_cache=no])

AS_IF([test "x$enable_cache" = "xyes"],
      [
      AC_CHECK_PROG([NBTK_CREATE_IMAGE_CACHE],
                [nbtk-create-image-cache],
                [$(which nbtk-create-image-cache)])
])

AM_CONDITIONAL([ENABLE_CACHE],   [test "x$enable_cache" = "xyes"])

AC_ARG_ENABLE([meego-desktop-file],
              [AC_HELP_STRING([--disable-meego-desktop-file],
                              [Disable installation of meego desktop file])],
              [enable_mdesktop=$enableval],
              [enable_mdesktop=yes])

AM_CONDITIONAL([ENABLE_MEEGO_DESKTOP_FILE], [test "x$enable_mdesktop" = "xyes"])

AC_OUTPUT([
        Makefile
        src/Makefile
        data/Makefile
        data/style/Makefile
        po/Makefile.in
])
