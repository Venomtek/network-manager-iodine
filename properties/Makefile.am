plugindir = $(libdir)/NetworkManager
plugin_LTLIBRARIES = libnm-vpn-plugin-iodine.la
if WITH_GNOME
plugin_LTLIBRARIES += libnm-iodine-properties.la
endif

libnm_vpn_plugin_iodine_la_SOURCES =                    \
        nm-iodine.c                                     \
        nm-iodine.h

editor_sources =                                        \
        nm-iodine.c                                     \
        nm-iodine.h

libnm_iodine_properties_la_SOURCES =                    \
        $(editor_sources)

uidir = $(datadir)/gnome-vpn-properties/iodine
ui_DATA = nm-iodine-dialog-gtk3.ui                      \
          nm-iodine-dialog-gtk4.ui

common_CFLAGS =                                         \
	-I$(top_srcdir)/src				\
        -DICONDIR=\""$(datadir)/pixmaps"\"              \
        -DUIDIR=\""$(uidir)"\"                          \
        -DG_DISABLE_DEPRECATED                          \
        -DGDK_DISABLE_DEPRECATED                        \
        -DGNOME_DISABLE_DEPRECATED                      \
        -DGNOMELOCALEDIR=\"$(datadir)/locale\"		\
        -DVERSION=\"$(VERSION)\"

libnm_vpn_plugin_iodine_la_CFLAGS =                     \
        -DUIFILE=\"nm-iodine-dialog-gtk3.ui\"           \
        $(GTK_CFLAGS)                                   \
        $(LIBNM_CFLAGS)                                 \
        $(LIBNMA_CFLAGS)                                \
        $(common_CFLAGS)

libnm_iodine_properties_la_CFLAGS =                     \
        -DUIFILE=\"nm-iodine-dialog-gtk3.ui\"           \
        $(GTK_CFLAGS)                                   \
        $(LIBNM_CFLAGS)                                 \
        $(common_CFLAGS)

libnm_vpn_plugin_iodine_la_LIBADD =                     \
        $(GTK_LIBS)                                     \
        $(LIBNMA_LIBS)                                  \
        $(LIBNM_LIBS)

libnm_iodine_properties_la_LIBADD =                     \
        $(GTK_LIBS)

libnm_vpn_plugin_iodine_la_LDFLAGS =                    \
        -avoid-version

libnm_iodine_properties_la_LDFLAGS =                    \
        $(libnm_vpn_plugin_iodine_la_LDFLAGS)


if WITH_GTK4
plugin_LTLIBRARIES += libnm-gtk4-vpn-plugin-iodine-editor.la
endif

libnm_gtk4_vpn_plugin_iodine_editor_la_SOURCES =        \
        $(editor_sources)

libnm_gtk4_vpn_plugin_iodine_editor_la_CFLAGS =         \
        -DUIFILE=\"nm-iodine-dialog-gtk4.ui\"           \
        $(GTK4_CFLAGS)                                  \
        $(LIBNM_CFLAGS)                                 \
        $(common_CFLAGS)

libnm_gtk4_vpn_plugin_iodine_editor_la_LIBADD =         \
        $(GTK_LIBS)

libnm_gtk4_vpn_plugin_iodine_editor_la_LDFLAGS =        \
        -avoid-version

CLEANFILES = *.bak *~

EXTRA_DIST =                            \
        $(ui_DATA)
