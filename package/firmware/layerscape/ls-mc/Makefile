#
# Copyright 2017 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ls-mc
PKG_VERSION:=10.39.104
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/NXP/qoriq-mc-binary.git
PKG_MIRROR_HASH:=0c08686db2dabb6f97471f858e9364cc81c9a77e1a9149584f3c78ee40d55e7c

PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

define Package/layerscape-mc
  SECTION:=firmware
  CATEGORY:=Firmware
  TITLE:=NXP MC firmware
  DEPENDS:=@TARGET_layerscape
  DEFAULT:=y if TARGET_layerscape_armv8_64b
  HIDDEN:=1
endef

define Build/Compile
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(CP) $(PKG_BUILD_DIR)/ls1088a/mc_ls1088a_$(PKG_VERSION).itb \
		$(STAGING_DIR_IMAGE)/fsl_ls1088a-rdb-mc.itb
	$(CP) $(PKG_BUILD_DIR)/ls2088a/mc_ls2088a_$(PKG_VERSION).itb \
		$(STAGING_DIR_IMAGE)/fsl_ls2088a-rdb-mc.itb
	$(CP) $(PKG_BUILD_DIR)/lx216xa/mc_lx2160a_$(PKG_VERSION).itb \
		$(STAGING_DIR_IMAGE)/fsl_lx2160a-rdb-mc.itb
endef

$(eval $(call BuildPackage,layerscape-mc))
