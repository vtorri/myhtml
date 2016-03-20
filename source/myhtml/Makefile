TARGET := source/myhtml
SRCDIR := source/myhtml

CC ?= gcc

LIBPOSTFIX := .so
LIBNAME    := myhtml
LIBSTATIC_PREFIX  := static_

MyHTML_OPTIMIZATION_LEVEL ?= -O2

CFLAGS ?= -Wall -Werror
CFLAGS += $(MyHTML_OPTIMIZATION_LEVEL) -fPIC --std=c99 -I..

MyHTML_BUILD_WITHOUT_THREADS ?= NO
ifeq ($(MyHTML_BUILD_WITHOUT_THREADS),YES)
    $(info Build without POSIX Threads)
	CFLAGS += -DMyHTML_BUILD_WITHOUT_THREADS
else
    $(info Build with POSIX Threads)
	CFLAGS += -pthread
endif

ifeq ($(OS),Windows_NT)
else
	UNAM := $(shell uname -s)
	ifeq ($(UNAM),Darwin)
		LIBPOSTFIX := .dylib
	else
		CFLAGS += -D_POSIX_C_SOURCE=199309L
	endif
endif

SRCS := $(wildcard *.c)
SRCS += $(wildcard utils/*.c)
HDRS := $(wildcard *.h)
HDRS += $(wildcard utils/*.h)
OBJS := $(patsubst %.c, %.o, $(SRCS))

all: shared static

shared: $(OBJS) $(HDRS)
	$(CC) -shared $(LDFLAGS) $(OBJS) -o lib$(LIBNAME)$(LIBPOSTFIX)

static: shared
	$(AR) crus $(LIBSTATIC_PREFIX)lib$(LIBNAME).a $(OBJS)

clean:
	rm -rf *.o
	rm -rf utils/*.o
	rm -rf *lib$(LIBNAME)*

.PHONY: all clean