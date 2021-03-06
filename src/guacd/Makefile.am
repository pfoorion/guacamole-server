#
# Copyright (C) 2013 Glyptodon LLC
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.
#

AUTOMAKE_OPTIONS = foreign 

AM_CFLAGS = -Werror -Wall -pedantic @LIBGUAC_INCLUDE@ @COMMON_INCLUDE@

sbin_PROGRAMS = guacd

man_MANS =           \
    man/guacd.8      \
    man/guacd.conf.5

noinst_HEADERS =  \
    client.h      \
    client-map.h  \
    conf-args.h   \
    conf-file.h   \
    conf-parse.h  \
    log.h

guacd_SOURCES =   \
    daemon.c      \
	client.c      \
	client-map.c  \
	conf-args.c   \
	conf-file.c   \
	conf-parse.c  \
	log.c

guacd_LDADD   = @LIBGUAC_LTLIB@ @COMMON_LTLIB@
guacd_LDFLAGS = @PTHREAD_LIBS@ @SSL_LIBS@

EXTRA_DIST = init.d/guacd.in man/guacd.8
CLEANFILES = $(init_SCRIPTS)

# SSL support
if ENABLE_SSL
noinst_HEADERS += socket-ssl.h
guacd_SOURCES  += socket-ssl.c
endif

# Init script
if ENABLE_INIT
initdir = @init_dir@
init_SCRIPTS = init.d/guacd

init.d/guacd: init.d/guacd.in
	sed -e 's,[@]sbindir[@],$(sbindir),g' < init.d/guacd.in > init.d/guacd
	chmod +x init.d/guacd
endif

