#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2013 Alexander Pyhalov
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		evolution
COMPONENT_VERSION=	2.32.3
COMPONENT_PROJECT_URL=	https://projects.gnome.org/evolution/
COMPONENT_SUMMARY=	Evolution Email and Calendar
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH=	\
    sha256:33ab38780e9abb71506230e331e9c3534444b5ed3f17046f0b6371a00df686fb
COMPONENT_ARCHIVE_URL=	http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/2.32/$(COMPONENT_NAME)-$(COMPONENT_VERSION).tar.bz2

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PATH=/usr/gnu/bin:/usr/bin:/usr/perl5/bin

COMPONENT_PRE_CONFIGURE_ACTION =        (cp -r $(SOURCE_DIR)/* $(@D) && \
					cp -r $(COMPONENT_DIR)/files/po-sun $(@D) && \
					cd $(@D)/po-sun && $(MAKE) all &&\
					cd $(@D) && glib-gettextize --force --copy &&\
					intltoolize --force --copy --automake &&\
					aclocal -I ./m4 &&\
					autoheader &&\
					automake -a -f -c --gnu &&\
					autoconf )
					
CONFIGURE_SCRIPT=       $(@D)/configure

gcc_OPT		= -O2

LDFLAGS+=       -L/usr/lib/mps -R/usr/lib/mps

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--libexecdir=/usr/lib
CONFIGURE_OPTIONS+=	--localstatedir=/var
CONFIGURE_OPTIONS+=	--enable-nss=yes
CONFIGURE_OPTIONS+=	--enable-smime=yes
CONFIGURE_OPTIONS+=	--enable-pilot-conduits=no
CONFIGURE_OPTIONS+=	--with-pisock=yes
CONFIGURE_OPTIONS+=	--with-sunldap=/usr
CONFIGURE_OPTIONS+=	--with-krb5=/usr
CONFIGURE_OPTIONS+=	--disable-nm
CONFIGURE_OPTIONS+=	--disable-pst-import
CONFIGURE_OPTIONS+=	--disable-image-inline

COMPONENT_INSTALL_ENV+=	GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TESTS)

BUILD_PKG_DEPENDENCIES = $(BUILD_TOOLS)

include $(WS_TOP)/make-rules/depend.mk
