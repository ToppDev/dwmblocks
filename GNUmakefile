PREFIX = /usr/local

CC = gcc
CFLAGS = -O3 -Wall -Wextra

X11CFLAGS = $(shell pkg-config --cflags x11)
X11LIBS = $(shell pkg-config --libs x11)

all: dwmblocks sigdwmblocks/sigdwmblocks xgetrootname/xgetrootname

dwmblocks: dwmblocks.c config.h block.h
	${CC} -o $@ -Wno-missing-field-initializers -Wno-unused-parameter ${CFLAGS} ${X11CFLAGS} $< ${X11LIBS}

sigdwmblocks/sigdwmblocks: sigdwmblocks/sigdwmblocks.c
	${CC} -o $@ ${CFLAGS} $<

xgetrootname/xgetrootname: xgetrootname/xgetrootname.c
	${CC} -o $@ ${CFLAGS} ${X11CFLAGS} $< ${X11LIBS}

clean:
	rm -f dwmblocks sigdwmblocks/sigdwmblocks xgetrootname/xgetrootname

BINDIR = ${DESTDIR}${PREFIX}/bin
PIDDIR = ${DESTDIR}/var/local/dwmblocks

install: all
	mkdir -p ${BINDIR}
	cp -f dwmblocks sigdwmblocks/sigdwmblocks xgetrootname/xgetrootname ${BINDIR}
	chmod 755 ${BINDIR}/dwmblocks ${BINDIR}/sigdwmblocks ${BINDIR}/xgetrootname
	mkdir -p ${PIDDIR}
	chmod 777 ${PIDDIR}

uninstall:
	rm -f ${BINDIR}/dwmblocks ${BINDIR}/sigdwmblocks ${BINDIR}/xgetrootname
	rm -df ${PIDDIR} || exit 0

.PHONY: all clean install uninstall
