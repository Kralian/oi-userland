#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2014 Josef 'Jeff' Sipek <jeffpc@josefsipek.net>
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		openttd
COMPONENT_VERSION=	1.4.3
COMPONENT_PROJECT_URL=	http://www.openttd.org/en/
COMPONENT_FMRI=		games/openttd
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC)-source.tar.gz
COMPONENT_ARCHIVE_HASH=	\
	sha256:51e3c445783dbba24d4a8490c7f33086a4523ccbd0457543b9f86ff9080e7eca
COMPONENT_ARCHIVE_URL=	http://binaries.openttd.org/releases/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=	GPLv2
COMPONENT_LICENSE_FILE=	$(COMPONENT_NAME).license
COMPONENT_SUMMARY=	OpenTTD is an open source simulation game based upon Transport Tycoon Deluxe

CONFIGURE_DEFAULT_DIRS=no

include ../../make-rules/prep.mk
include ../../make-rules/configure.mk
include ../../make-rules/ips.mk

CONFIGURE_OPTIONS += --prefix-dir=$(CONFIGURE_PREFIX)
CONFIGURE_OPTIONS += --binary-dir=bin
CONFIGURE_OPTIONS += --data-dir=share/openttd
CONFIGURE_OPTIONS += --install-dir=$(PROTO_DIR)
CONFIGURE_OPTIONS += --disable-strip
CONFIGURE_OPTIONS += --without-allegro
CONFIGURE_OPTIONS += --with-sdl
CONFIGURE_OPTIONS += --with-zlib
CONFIGURE_OPTIONS += --with-liblzma
CONFIGURE_OPTIONS += --with-liblzo2
CONFIGURE_OPTIONS += --with-png
CONFIGURE_OPTIONS += --with-freetype
CONFIGURE_OPTIONS += --with-fontconfig
CONFIGURE_OPTIONS += --without-icu
CONFIGURE_OPTIONS += --without-iconv
CONFIGURE_OPTIONS += --without-menu-entry

COMPONENT_BUILD_ARGS += DO_NOT_INSTALL_CHANGE_LOG=1
COMPONENT_BUILD_ARGS += DO_NOT_INSTALL_LICENSE=1

COMPONENT_PRE_CONFIGURE_ACTION=$(CLONEY) $(SOURCE_DIR) $(@D)

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(TEST_32)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

include ../../make-rules/depend.mk
