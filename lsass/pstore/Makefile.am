SUBDIRS = . test plugin

AM_CPPFLAGS += -I$(top_srcdir)/include

lib_LTLIBRARIES = liblsapstore.la

liblsapstore_la_SOURCES =  \
        lsapstore-backend-legacy.c \
        lsapstore-backend-legacy-internal.c \
        lsapstore-init.c \
        lsapstore-main.c \
        lsapstore-main-a.c \
        lsapstore-plugin.c \
        lsapstore-utils.c

liblsapstore_la_LIBADD = \
        $(DL_LIBS) \
        $(PTHREAD_LIBS) \
        $(LWREG_LIBS) \
        $(LWBASE_NOTHR_LIBS) \
        @top_builddir@/common/liblsacommon.la

liblsapstore_la_LDFLAGS = \
     -export-symbols=lsapstore.sym
