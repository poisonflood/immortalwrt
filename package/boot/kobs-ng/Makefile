#
# Copyright (C) 2013-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=kobs-ng
PKG_VERSION:=5.5
PKG_RELEASE:=1

PKG_SOURCE:=imx-kobs-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.freescale.com/lgfiles/NMG/MAD/YOCTO/
PKG_HASH:=57faac9ce124f08dafc16501f229ef954994daa08eda11db9c23c4983055da90
PKG_BUILD_DIR:=$(BUILD_DIR)/imx-kobs-$(PKG_VERSION)

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=COPYING
PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

define Package/kobs-ng
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Application for writing bootstreams to NAND flash
  DEPENDS:=@TARGET_imx
endef

define Package/kobs-ng/description
 The kobs-ng application writes a bootstream to NAND flash with the proper
 FCB/DBBT headers and replicated streams.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	echo "const char* git_sha = \"$(PKG_VERSION)\";" > $(PKG_BUILD_DIR)/autoversion.h
endef

define Package/kobs-ng/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/kobs-ng $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,kobs-ng))
