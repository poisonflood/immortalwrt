#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libtool
PKG_VERSION:=2.5.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNU/libtool
PKG_HASH:=f81f5860666b0bc7d84baddefa60d1cb9fa6fceb2398cc3baca6afaa60266675

PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:gnu:libtool

PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

CONFIGURE_PREFIX=$(STAGING_DIR_HOSTPKG)
export GLOBAL_LIBDIR=$(STAGING_DIR)/usr/lib

define Package/libltdl
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A generic dynamic object loading library
  URL:=http://www.gnu.org/software/libtool/
  ABI_VERSION:=7
endef

define Build/InstallDev
	$(MAKE) -C $(PKG_BUILD_DIR) \
		bindir="$(2)/libltdl/bin" \
		datadir="$(2)/libltdl/share" \
		prefix="$(2)/libltdl" \
		exec_prefix="$(2)/libltdl" \
		install
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/include
	mv $(2)/libltdl/lib/* $(1)/usr/lib/
	mv $(2)/libltdl/include/* $(1)/usr/include/
endef

define Package/libltdl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libltdl/.libs/libltdl.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libltdl))
