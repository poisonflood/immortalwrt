# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2015 OpenWrt.org
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wpan-tools
PKG_VERSION:=0.10
PKG_RELEASE=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/linux-wpan/wpan-tools/releases/download/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_NAME)-$(PKG_VERSION).tar.gz?
PKG_HASH:=301dc7d1f16438154eb0aa0c1bc6c7b0fcacb92ca0dc699de3debbcb205f5f26

include $(INCLUDE_DIR)/package.mk

define Package/wpan-tools
  SECTION:=net
  CATEGORY:=Network
  TITLE:=cfg802154 interface configuration utility
  URL:=https://linux-wpan.org/wpan-tools.html
  DEPENDS:= +libnl
endef

define Package/wpan-tools/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/iwpan $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wpan-ping/wpan-ping $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,wpan-tools))
