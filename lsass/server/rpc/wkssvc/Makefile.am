srv_srcdir = $(top_srcdir)/server
rpc_srcdir = $(srv_srcdir)/rpc
idl_srcdir = $(top_srcdir)/idl

if ENABLE_STATIC_RPCSERVERS
noinst_LTLIBRARIES = libwkssvc_srv.la
else
rpcserver_LTLIBRARIES = libwkssvc_srv.la
noinst_LTLIBRARIES = libwkssvc_ss.la libwkssvc.la
endif

libwkssvc_la_SOURCES =          \
    globals.c                   \
    wkssvc.c                    \
    wkss_cfg.c                  \
    wkss_srv.c                  \
    wkss_memory.c               \
    wkss_accesstoken.c          \
    wkss_crypto.c               \
    wkss_security.c             \
    netr_wkstagetinfo.c         \
    netr_wkstauserenum.c        \
    netr_joindomain2.c          \
    netr_unjoindomain2.c

DCEIDL_PASS_INCLUDES =         \
    $(CPPFLAGS)                \
    $(LWBASE_INCLUDES)         \
    -I$(top_srcdir)/include

libwkssvc_la_CFLAGS =        \
    $(AM_CFLAGS)             \
    -I$(srv_srcdir)/include  \
    -I$(top_srcdir)/include  \
    -I$(rpc_srcdir)/samr     \
    -I$(srv_srcdir)/api      \
    $(DCERPC_INCLUDES)       \
    $(LWBASE_INCLUDES)       \
    $(LWADVAPI_INCLUDES)     \
    $(NETLOGON_INCLUDES)

libwkssvc_la_LIBADD =                             \
    $(DCERPC_LIBS)                                \
    $(LWBASE_LIBS)                                \
    $(LWADVAPI_LIBS)                              \
    $(NETLOGON_LIBS)                              \
    $(top_builddir)/server/api/liblsaserverapi.la \
    $(top_builddir)/client/rpc/liblsarpc.la

libwkssvc_ss_la_SOURCES = \
    wkssvc_sstub.c

libwkssvc_ss_la_CFLAGS =     \
    $(AM_CFLAGS)          \
    -DDCERPC_STUB_BUILD   \
    $(FEATURETEST_FLAGS)  \
    $(DCERPC_INCLUDES)    \
    $(LWBASE_INCLUDES)

libwkssvc_ss_la_LIBADD = \
    libwkssvc.la

libwkssvc_srv_la_SOURCES =
libwkssvc_srv_la_CFLAGS = \
    $(AM_CFLAGS)
libwkssvc_srv_la_LIBADD = \
    libwkssvc_ss.la
libwkssvc_srv_la_LDFLAGS = -module -avoid-version

CLEAN_FILES = wkssvc_cstub.c wkssvc_sstub.c wkssvc_h.h

BUILT_SOURCES = wkssvc_h.h

wkssvc_sstub.c wkssvc_cstub.c wkssvc_h.h: $(idl_srcdir)/wkssvc.idl wkssvc.acf
	$(IDL) $(IDLFLAGS) -keep c_source -header wkssvc_h.h -cstub_pref cli_ -sstub_pref srv_ \
                -I$(srcdir) -I$(idl_srcdir) $(DCEIDL_PASS_INCLUDES) $<
