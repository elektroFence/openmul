ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

pkgconfigdir=$(libdir)/pkgconfig

bin_PROGRAMS = mulmtrack

LIB_GLIB = @LIB_GLIB@
LIB_EVENT = @LIB_EVENT@
GLIB_INCLUDE = @GLIB_INCLUDE@
LIBEVENT_INCLUDE = @LIBEVENT_INCLUDE@

INCLUDES = -I. -I$(top_srcdir)/mul -I$(top_srcdir)/common/ \
           -I$(top_srcdir)/services/loadable/topo_routing/ \
           -I$(top_srcdir)/common-libs/3rd-party/derived-lib/include/ \
           -I$(top_srcdir)/common-libs/3rd-party/quagga-lib/include/ \
           -I$(top_srcdir)/common-libs/mul-lib/include/ \
            -I$(top_srcdir)/common-libs/util-linux/libuuid/src/

DEFS = @DEFS@ -DSYSCONFDIR=\"$(sysconfdir)/\"

mulmtrack_CFLAGS = -DMUL_APP_V2_MLAPI

mulmtrack_SOURCES = memtrack.c $(top_srcdir)/common/mul_app_main.c

LD_FLAGS= @LDFLAGS@ 

if !HAVE_EXT_GLIB
LD_FLAGS += -Wl,-rpath=$(LIB_GLIB) -L$(LIB_GLIB)
INCLUDES += -I$(GLIB_INCLUDE) -I$(GLIB_INCLUDE)/../
endif

if !HAVE_EXT_LIBEVENT
LD_FLAGS += -Wl,-rpath=$(LIB_EVENT) -L$(LIB_EVENT)
INCLUDES += -I$(LIBEVENT_INCLUDE)
endif

mulmtrack_LDADD = \
                $(top_srcdir)/common-libs/mul-lib/.libs/libmulutil.a  \
                $(top_srcdir)/services/loadable/topo_routing/./.libs/libmultr.a -lrt \
                -lcrypto -lssl -lglib-2.0

mulmtrack_LDFLAGS = $(LD_FLAGS) -lpthread -levent -lcrypt

noinst_HEADERS = memtrack.h
