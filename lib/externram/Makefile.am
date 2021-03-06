include_HEADERS = externRAMClientWrapper.h

noinst_LTLIBRARIES = libexternramClientImpl.la

EXTERNRAM_FLAGS =
if ! DEBUG
EXTERNRAM_FLAGS += -DNDEBUG
if PROFILING
EXTERNRAM_FLAGS += -g
endif
else
if RAMCLOUD
EXTERNRAM_FLAGS += -DRAMCLOUD_DEBUG
else
EXTERNRAM_FLAGS += -DDEBUG
endif
endif
if TRACE
EXTERNRAM_FLAGS += -DTRACE
endif
if THREADED_WRITE_TO_EXTERNRAM
EXTERNRAM_FLAGS += -DTHREADED_WRITE_TO_EXTERNRAM
endif
if THREADED_PREFETCH
EXTERNRAM_FLAGS += -DTHREADED_PREFETCH
endif
if LOCK_DEBUG
EXTERNRAM_FLAGS += -DLOCK_DEBUG
endif
if ASYNREAD
EXTERNRAM_FLAGS += -DASYNREAD
endif
if TIMING
EXTERNRAM_FLAGS += -DTIMING
endif

libexternramClientImpl_la_SOURCES = externRAMClient.hh
libexternramClientImpl_la_CPPFLAGS = -std=c++0x -I$(SCALEOS_ROOT)/include -I$(SCALEOS_ROOT)/lib/monitorstats -I$(SCALEOS_ROOT)/lib/userfault $(EXTERNRAM_FLAGS)
libexternramClientImpl_la_LDFLAGS = -L$(SCALEOS_ROOT)/lib/monitorstats/.libs \
  -Wl,-rpath,$(SCALEOS_ROOT)/lib/monitorstats/.libs
libexternramClientImpl_la_LIBADD = -lmonitorstats
if RAMCLOUD
libexternramClientImpl_la_SOURCES += ramcloud/externRAMClientImpl.hh ramcloud/externRAMClientImpl.cc
libexternramClientImpl_la_CPPFLAGS += -I/include/ramcloud -I/include/gtest/include
libexternramClientImpl_la_LDFLAGS += -L/lib/ramcloud -Wl,-rpath,/lib/ramcloud
libexternramClientImpl_la_LIBADD += -lramcloud \
  -lboost_system \
  -lprotobuf \
  -lzookeeper_mt \
  -lpcrecpp \
  -libverbs
endif

if MEMCACHED
libexternramClientImpl_la_SOURCES += memcached/externRAMClientImpl.hh memcached/externRAMClientImpl.cc
libexternramClientImpl_la_LIBADD += -lmemcached \
  -lmemcachedutil \
  -lpthread
endif

if NOOP
libexternramClientImpl_la_SOURCES += noop/externRAMClientImpl.hh noop/externRAMClientImpl.cc
libexternramClientImpl_la_LIBADD += -lboost_system
endif

lib_LTLIBRARIES = libexternram.la
libexternram_la_SOURCES = externRAMClientWrapper.h externRAMClientWrapper.cc
libexternram_la_LIBADD = libexternramClientImpl.la

AM_CPPFLAGS =

if ! CCACHE
AM_CPPFLAGS += -DCACHE
endif
if DEBUG
AM_CPPFLAGS += -g -DDEBUG
else
AM_CPPFLAGS += -DNDEBUG
if PROFILING
AM_CPPFLAGS += -g
endif
endif
if TRACE
AM_CPPFLAGS += -DTRACE
endif
if THREADED_WRITE_TO_EXTERNRAM
AM_CPPFLAGS += -DTHREADED_WRITE_TO_EXTERNRAM
endif
if THREADED_PREFETCH
AM_CPPFLAGS += -DTHREADED_PREFETCH
endif
if LOCK_DEBUG
AM_CPPFLAGS += -DLOCK_DEBUG
endif
if ASYNREAD
AM_CPPFLAGS += -DASYNREAD
endif
if TIMING
AM_CPPFLAGS += -DTIMING
endif

