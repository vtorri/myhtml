TARGET := examples
SRCDIR := examples

CC ?= gcc
LIBS := ../lib/static_libmyhtml.a

ifeq ($(OS),Windows_NT)
else
	UNAM := $(shell uname -s)
	ifeq ($(UNAM),Darwin)
		CFLAGS := -Wall -Werror -O2 --std=c99 -I../include $(LIBS)
	else
		CFLAGS := -Wall -Werror -O2 --std=c99 -pthread -D_POSIX_C_SOURCE=199309L -I../include $(LIBS)
	endif
endif

SRCS := $(wildcard *.c)
OBJS := $(patsubst %.c, %, $(SRCS))

all: $(TARGET)

$(TARGET): $(OBJS)
	cp $< ../bin/

clean:
	rm -f `ls | grep -v '.c\|Makefile$\'`
	rm -f ../bin/*
.PHONY: all clean