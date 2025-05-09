# SPDX-License-Identifier: GPL-2.0-or-later
#
# Copyright 2020 NXP
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ls-ddr-phy
PKG_VERSION:=6.12.3.1.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/NXP/ddr-phy-binary.git
PKG_SOURCE_VERSION:=lf-6.12.3-1.0.0
PKG_MIRROR_HASH:=1608b12558d613bff6aee7071f6af8c08e4ba50ddb6b3356cf472bb52670cae8
#PKG_BUILD_DEPENDS:=tfa-layerscape/host

PKG_LICENSE:=EULA
PKG_LICENSE_FILES:=NXP-Binary-EULA.txt

PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

define Package/layerscape-ddr-phy
  SECTION:=firmware
  CATEGORY:=Firmware
  TITLE:=NXP Layerscape DDR PHY firmware
  DEPENDS:=@TARGET_layerscape
  DEFAULT:=y if TARGET_layerscape_armv8_64b
  HIDDEN:=1
endef

define Build/Compile
	cd $(PKG_BUILD_DIR)/lx2160a/ && \
	fiptool-layerscape create \
		--ddr-immem-udimm-1d ddr4_pmu_train_imem.bin \
		--ddr-immem-udimm-2d ddr4_2d_pmu_train_imem.bin \
		--ddr-dmmem-udimm-1d ddr4_pmu_train_dmem.bin \
		--ddr-dmmem-udimm-2d ddr4_2d_pmu_train_dmem.bin \
		--ddr-immem-rdimm-1d ddr4_rdimm_pmu_train_imem.bin \
		--ddr-immem-rdimm-2d ddr4_rdimm2d_pmu_train_imem.bin \
		--ddr-dmmem-rdimm-1d ddr4_rdimm_pmu_train_dmem.bin \
		--ddr-dmmem-rdimm-2d ddr4_rdimm2d_pmu_train_dmem.bin \
		fip_ddr_all.bin
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(CP) $(PKG_BUILD_DIR)/lx2160a/fip_ddr_all.bin \
		$(STAGING_DIR_IMAGE)/fsl_lx2160a-rdb-fip_ddr_all.bin
endef

$(eval $(call BuildPackage,layerscape-ddr-phy))
