#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2014 Alexander Pyhalov.  All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= xorg-server
COMPONENT_VERSION= 1.7.7
COMPONENT_SUMMARY= Xorg - X11R7 X server
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH= \
  sha256:54c4d32bfeb8852adbea3ddae6981f3bc2eadb330124d9b35226c617c01926ff
COMPONENT_ARCHIVE_URL= \
  http://ftp.x.org/pub/individual/xserver/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.x.org/wiki/
COMPONENT_CLASSIFICATION= System/X11
COMPONENT_LICENSE_FILE = COPYING
COMPONENT_LICENSE = MIT

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

COMPONENT_POST_UNPACK_ACTION +=  ( cp -r $(COMPONENT_DIR)/srcs/* $(SOURCE_DIR))

# Missing files in build dir for configure without this.
COMPONENT_PRE_CONFIGURE_ACTION =        (cp -a $(SOURCE_DIR)/* $(@D) &&\
		cd $(@D) && autoreconf --install --force )

# Enabling gcc optimization leads to crashes
gcc_OPT = 

PATCH_LEVEL=0

SERVERMOD_SUBDIR.64=/$(MACH64)
SERVERMOD_SUBDIR=$(SERVERMOD_SUBDIR.$(BITS))
X11_SERVERMODS_DIR=/usr/lib/xorg/modules
X11_SERVERLIBS_DIR=/usr/lib/xorg

CPPFLAGS += -DSUNSOFT -DTSOL

CONFIGURE_SCRIPT = $(@D)/configure

CONFIGURE_OPTIONS.32 += --bindir=/usr/bin
CONFIGURE_OPTIONS.64 += --bindir=/usr/bin/$(MACH64)

CONFIGURE_OPTIONS = $(CONFIGURE_OPTIONS.$(BITS))
CONFIGURE_OPTIONS += --disable-install-setuid
CONFIGURE_OPTIONS += --disable-shave
CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --disable-unit-tests
CONFIGURE_OPTIONS += --disable-xsdl
CONFIGURE_OPTIONS += --disable-xwin
CONFIGURE_OPTIONS += --disable-xnest
CONFIGURE_OPTIONS += --enable-builddocs
CONFIGURE_OPTIONS += --enable-dri2
CONFIGURE_OPTIONS += --enable-glx
CONFIGURE_OPTIONS += --enable-kdrive
CONFIGURE_OPTIONS += --enable-shared
CONFIGURE_OPTIONS += --enable-xcsecurity
CONFIGURE_OPTIONS += --enable-xephyr
CONFIGURE_OPTIONS += --enable-xdm-auth-1
CONFIGURE_OPTIONS += --enable-xdmcp
CONFIGURE_OPTIONS += --prefix=/usr
CONFIGURE_OPTIONS += --with-builderstring="Solaris ABI: $(BITS)-bit"
CONFIGURE_OPTIONS += --with-default-font-path='catalogue:/etc/X11/fontpath.d'
CONFIGURE_OPTIONS += --with-dri-driver-path='$(X11_SERVERMODS_DIR)/dri$(SERVERMOD_SUBDIR)'
CONFIGURE_OPTIONS += --with-default-xkb-model=pc105
CONFIGURE_OPTIONS += --with-log-dir=/var/log
CONFIGURE_OPTIONS += --with-module-dir=/usr/lib/xorg/modules$(SERVERMOD_SUBDIR)
CONFIGURE_OPTIONS += --with-os-name="`uname -srm`"
CONFIGURE_OPTIONS += --with-vendor-name="Project OpenIndiana"
CONFIGURE_OPTIONS += --with-vendor-web="http://openindiana.org"
CONFIGURE_OPTIONS += --with-xkb-output=/var/run/xkb
CONFIGURE_OPTIONS += --with-xkb-bin-directory=/usr/bin

CONFIGURE_ENV += CPPFLAGS="$(CPPFLAGS)"

COMPONENT_BUILD_ENV += SERVERMOD_SUBDIR="$(SERVERMOD_SUBDIR)"

COMPONENT_POST_BUILD_ACTION += ( $(ENV) $(COMPONENT_BUILD_ENV) $(CONFIGURE_ENV) $(MAKE) -C $(BUILD_DIR_$(BITS))/os/solaris/mdb )
COMPONENT_POST_INSTALL_ACTION += ( $(ENV) $(COMPONENT_BUILD_ENV) $(CONFIGURE_ENV) $(MAKE) $(COMPONENT_INSTALL_ARGS) \
			-C $(BUILD_DIR_$(BITS))/os/solaris/mdb install )

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)
