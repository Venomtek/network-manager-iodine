AC_PREREQ([2.71])

AC_INIT([NetworkManager-iodine],[1.2.1],[agx@sigxcpu.org],[NetworkManager-iodine])
AM_INIT_AUTOMAKE([subdir-objects no-dist-gzip dist-xz])
AM_MAINTAINER_MODE

AC_CONFIG_MACRO_DIR([m4])

AC_CONFIG_HEADERS([config.h])

dnl
dnl Require programs
dnl
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_INSTALL
LT_INIT

dnl
dnl Required headers
dnl
AC_CHECK_HEADERS(fcntl.h paths.h sys/ioctl.h sys/time.h syslog.h unistd.h)

dnl
dnl Checks for typedefs, structures, and compiler characteristics.
dnl
AC_TYPE_MODE_T
AC_TYPE_PID_T

dnl
dnl Checks for library functions.
dnl
AC_PROG_GCC_TRADITIONAL
AC_FUNC_MEMCMP
AC_CHECK_FUNCS(select socket uname)

dnl
dnl GNOME support
dnl
AC_ARG_WITH(gnome, AS_HELP_STRING([--without-gnome], [Build NetworkManager-iodine without GNOME support, e.g. vpn service only]))
AC_ARG_WITH(gtk4, AS_HELP_STRING([--with-gtk4], [Build NetworkManager-iodine with libnma-gtk4 support]), [], [with_gtk4_specified=no])
if test "$with_gnome" != no; then
        with_gnome=yes
fi
if test "$with_gtk4_specified" == no; then
        with_gtk4=no
fi
if test "$with_gtk4" != yes; then
        with_gtk4=no
fi
AM_CONDITIONAL(WITH_GNOME, test "$with_gnome" != no)
AM_CONDITIONAL(WITH_GTK4, test "$with_gtk4" != no)

AC_ARG_ENABLE(absolute-paths, AS_HELP_STRING([--enable-absolute-paths], [Use absolute paths to in .name files. Useful for development. (default is no)]))

GETTEXT_PACKAGE=NetworkManager-iodine
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE", [Gettext package])

IT_PROG_INTLTOOL([0.35])
AM_GLIB_GNU_GETTEXT
AC_PATH_PROG(GLIB_COMPILE_RESOURCES, glib-compile-resources)

PKG_CHECK_MODULES(GLIB, gmodule-2.0 glib-2.0 >= 2.34)
GLIB_CFLAGS="$GLIB_CFLAGS -DGLIB_VERSION_MIN_REQUIRED=GLIB_VERSION_2_34"
GLIB_CFLAGS="$GLIB_CFLAGS -DGLIB_VERSION_MAX_ALLOWED=GLIB_VERSION_2_34"

if test x"$with_gnome" != xno || test x"$with_gtk4" != xno; then
        PKG_CHECK_MODULES(LIBSECRET, libsecret-1 >= 0.18)
fi

if test x"$with_gnome" != xno; then
        PKG_CHECK_MODULES(GTK, gtk+-3.0 >= 3.4)
        GTK_CFLAGS="$GTK_CFLAGS -DGDK_VERSION_MIN_REQUIRED=GDK_VERSION_3_4"
        GTK_CFLAGS="$GTK_CFLAGS -DGDK_VERSION_MAX_ALLOWED=GDK_VERSION_3_4"
        PKG_CHECK_MODULES(LIBNMA, libnma >= 1.7.0)
fi

if test x"$with_gtk4" != xno; then
        PKG_CHECK_MODULES(GTK4, gtk4 >= 4.0)
        GTK4_CFLAGS="$GTK4_CFLAGS -DGDK_VERSION_MIN_REQUIRED=GDK_VERSION_4_0"
        GTK4_CFLAGS="$GTK4_CFLAGS -DGDK_VERSION_MAX_ALLOWED=GDK_VERSION_4_0"
        PKG_CHECK_MODULES(LIBNMA_GTK4, libnma-gtk4 >= 1.8.33)
fi

PKG_CHECK_MODULES(LIBNM, libnm >= 1.1.0)
LIBNM_CFLAGS="$LIBNM_CFLAGS -DNM_VERSION_MIN_REQUIRED=NM_VERSION_1_2"
LIBNM_CFLAGS="$LIBNM_CFLAGS -DNM_VERSION_MAX_ALLOWED=NM_VERSION_1_2"

NM_VPN_SERVICE_DIR=`$PKG_CONFIG --define-variable prefix='\${prefix}' --variable vpnservicedir libnm`
AC_SUBST(NM_VPN_SERVICE_DIR)

test x"$enable_absolute_paths" = x"yes" && NM_PLUGIN_DIR='$(libdir)/NetworkManager/'
AC_SUBST(NM_PLUGIN_DIR)

NM_COMPILER_WARNINGS

AC_CONFIG_FILES([
Makefile
src/Makefile
auth-dialog/Makefile
properties/Makefile
po/Makefile.in
])
AC_OUTPUT

echo ""
echo "Build configuration: "
echo "  --with-gnome=$with_gnome"
echo "  --with-gtk4=$with_gtk4"
echo ""

