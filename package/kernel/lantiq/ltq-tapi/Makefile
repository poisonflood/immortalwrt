#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=drv_tapi
PKG_VERSION:=4.7.3.6
PKG_RELEASE:=6

PKG_SOURCE:=drv_tapi-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@OPENWRT
PKG_HASH:=67fb46fed08cf505cb5d0b57ca58f06a8cba3247ff39a81048e310d1b77c96a7
PKG_MAINTAINER:=John Crispin <john@phrozen.org>

PKG_CHECK_FORMAT_SECURITY:=0
PKG_FIXUP:=autoreconf
PKG_EXTMOD_SUBDIRS:=src

include $(INCLUDE_DIR)/package.mk

define KernelPackage/ltq-tapi
  SUBMENU:=Voice over IP
  TITLE:=Lantiq TAPI subsystem
  URL:=http://www.lantiq.com/
  DEPENDS:=@(TARGET_lantiq_falcon||TARGET_lantiq_xway||TARGET_lantiq_xrx200) +kmod-ltq-ifxos
  FILES:=$(PKG_BUILD_DIR)/src/drv_tapi.ko
  AUTOLOAD:=$(call AutoLoad,20,drv_tapi)
endef

define KernelPackage/ltq-tapi/description
	Voice Subsystem Telephony API High Level Driver
endef

define KernelPackage/ltq-tapi/config
	source "$(SOURCE)/Config.in"
endef

MAKE_FLAGS += \
	$(KERNEL_MAKE_FLAGS)

CONFIGURE_ARGS += \
	ARCH=$(LINUX_KARCH) \
	--enable-linux-26 \
	--enable-kernelbuild="$(LINUX_DIR)" \
	--enable-kernelincl="$(LINUX_DIR)/include" \
	--with-ifxos-incl=$(STAGING_DIR)/usr/include/ifxos \
	$(call autoconf_bool,CONFIG_IFX_DRV_TAPI_EVENT_LOGGER,el-debug) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_FAX,fax t38) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_CID,cid) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_DECT,dect) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_KPI,kpi) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_QOS,qos) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_LT_GR909,lt) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_STATISTICS,statistics) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_METERING,metering) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_HDLC,hdlc) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_TRACES,trace) \
	$(call autoconf_bool,CONFIG_VOICE_CPE_TAPI_LINUX_HOTPLUG,hotplug)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/drv_tapi
	$(CP) --dereference $(PKG_BUILD_DIR)/include/* $(1)/usr/include/drv_tapi
	(cd $(1)/usr/include/drv_tapi && ln -s . include && ln -s ../ifxos/ifx_types.h .)
endef

$(eval $(call KernelPackage,ltq-tapi))
