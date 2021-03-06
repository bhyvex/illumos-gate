# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
#
# Copyright 2009 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#

DYNPROG= dsbitmap

include ../../Makefile.cmd
include ../Makefile.com

PROG = $(DYNPROG)

dsbitmap	:= POBJS = dsbitmap.o

OBJS=	dsbitmap.o
SRCS=	$(OBJS:%.o=%.c)
POFILE=	$(OBJS:%.o=%.po)

CFLAGS += $(CCVERBOSE)
CERRWARN += -_gcc=-Wno-uninitialized
LDLIBS += -lunistat -ladm
LINTFLAGS +=	-Xa -n -s -x -m -u -Dlint -errhdr=%user
LINTFLAGS +=	-erroff=E_SEC_PRINTF_VAR_FMT
ROOTLINK = $(ROOTUSRSBIN)/$(PROG)

all	:=	TARGET= all
install	:=	TARGET= install
clean	:=	TARGET= clean
clobber	:=	TARGET= clobber
lint	:=	TARGET= lint

.KEEP_STATE:

.PARALLEL: $(OBJS)

all:	$(PROG)

install: all $(ROOTPROG) $(ROOTLINK)

lint:	lint_SRCS

clean:
	$(RM) *.o $(POFILE)

$(PROG): $$(POBJS)
	$(LINK.c) $(POBJS) -o $@ $(LDLIBS)
	$(POST_PROCESS)

check:	$(PROG).c
	$(CSTYLE) -pP $(SRCS:%=%)

$(ROOTLINK): $(ROOTBIN)/$(PROG) $(ROOTUSRSBIN)
	-$(RM) $@; $(LN) $(ROOTBIN)/$(PROG) $@

FRC:

include ../../Makefile.targ
