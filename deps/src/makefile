# C compiler
CC=gcc
LINK=gcc
# C flags
CFLAGS=-fPIC -Wall -Wextra -O2 -g 
# linking flags
LDFLAGS=-shared
# rm command
RM=rm -f
# target lib
TARGET_LIB=libtriangle.so 
# Tridef
CFLAGS+=-DTRILIBRARY -DNO_TIMER

# source files
SRCS=tricall.c triangle.c 
OBJS=$(SRCS:.c=.o)

UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Linux)
    CFLAGS+=-DLINUX
endif

ifeq ($(UNAME_S),Darwin)
    LDFLAGS=-dynamiclib -undefined suppress -flat_namespace
endif

.PHONY: all
all: ${TARGET_LIB}

$(TARGET_LIB): $(OBJS)
	$(LINK) ${LDFLAGS} -o $@ $^

$(SRCS:.c=.d):%.d:%.c
	$(CC) $(CFLAGS) -MM $< >$@

include $(SRCS:.c=.d)

.PHONY: clean
clean:
	-${RM} ${TARGET_LIB} ${OBJS} $(SRCS:.c=.d)
