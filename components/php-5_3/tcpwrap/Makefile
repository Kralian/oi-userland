#
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
# Copyright (c) 2012, Oracle and/or its affiliates. All rights reserved.
#
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		tcpwrap
COMPONENT_VERSION=	1.1.3
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tgz
COMPONENT_ARCHIVE_HASH= \
    sha256:afd435399724b5032d2e65105a2c85a7fddb22bc5633571257299d32d46d9d54
COMPONENT_ARCHIVE_URL=	http://pecl.php.net/get/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	http://pecl.php.net/package/tcpwrap/

include ../extensions.mk

# The directory value for with-tcpwrap is tracking the
# location of libwrap.so without the "lib" part.

CONFIGURE_OPTIONS  += --with-tcpwrap=/usr

COMPONENT_POST_INSTALL_ACTION = ( \
	$(FIX_CONFIG_FILES_2); \
	)

PKG_PROTO_DIRS += $(COMPONENT_DIR)/../tcpwrap-zts/build/prototype/$(MACH)
