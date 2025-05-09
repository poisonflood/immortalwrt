#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libcap
PKG_VERSION:=2.76
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/linux/libs/security/linux-privs/libcap2
PKG_HASH:=629da4ab29900d0f7fcc36227073743119925fd711c99a1689bbf5c9b40c8e6f

PKG_MAINTAINER:=Paul Wassi <p.wassi@gmx.at>
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=License
PKG_CPE_ID:=cpe:/a:libcap_project:libcap

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/libcap/Default
  TITLE:=Linux capabilities library
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=https://www.kernel.org/pub/linux/libs/security/linux-privs/libcap2/
endef

define Package/libcap/description/Default
  Linux capabilities
endef

define Package/libcap
  $(call Package/libcap/Default)
  TITLE += library
endef

define Package/libcap-bin
  $(call Package/libcap/Default)
  TITLE += binaries
  DEPENDS += libcap
endef

define Package/libcap-bin/description
  $(call Package/libcap/description/Default)
  .
  This package contains the libcap utilities.
endef

define Package/libcap-bin/config
  if PACKAGE_libcap-bin
  config PACKAGE_libcap-bin-capsh-shell
    string "capsh shell"
    help
      Set the capsh shell.
    default "/bin/sh"
  endif
endef

MAKE_FLAGS += \
    BUILD_CC="$(CC)" \
    BUILD_CFLAGS="$(FPIC) -I$(PKG_BUILD_DIR)/libcap/include" \
    CFLAGS="$(TARGET_CFLAGS)" \
    LD="$(TARGET_CC) -Wl,-x -shared" \
    LDFLAGS="$(TARGET_LDFLAGS)" \
    INDENT="| true" \
    GOLANG="no" \
    PAM_CAP="no" \
    RAISE_SETFCAP="no" \
    DYNAMIC="yes" \
    lib="lib"

TARGET_CFLAGS += $(FPIC)

ifneq ($(CONFIG_PACKAGE_libcap-bin-capsh-shell),)
TARGET_CFLAGS += -DSHELL='\"$(CONFIG_PACKAGE_libcap-bin-capsh-shell)\"'
endif

TARGET_CFLAGS += $(if $(CONFIG_USE_MUSL),-Dpthread_yield=sched_yield)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/sys
	$(CP) $(PKG_INSTALL_DIR)/usr/include/sys/*.h $(1)/usr/include/sys/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/lib/libcap.{so*,a} $(1)/usr/lib/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/lib/libpsx.a $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/lib/pkgconfig/libcap.pc $(1)/usr/lib/pkgconfig/
	$(SED) 's,exec_prefix=,exec_prefix=/usr,g' $(1)/usr/lib/pkgconfig/libcap.pc
	$(SED) 's,/lib,$$$${exec_prefix}/lib,g' $(1)/usr/lib/pkgconfig/libcap.pc
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/libcap.pc
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/lib/pkgconfig/libpsx.pc $(1)/usr/lib/pkgconfig/
	$(SED) 's,exec_prefix=,exec_prefix=/usr,g' $(1)/usr/lib/pkgconfig/libpsx.pc
	$(SED) 's,/lib,$$$${exec_prefix}/lib,g' $(1)/usr/lib/pkgconfig/libpsx.pc
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/libpsx.pc
endef

define Package/libcap/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/lib/libcap.so* $(1)/usr/lib/
endef

define Package/libcap-bin/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/sbin/capsh     $(1)/usr/sbin/
	$(CP) $(PKG_INSTALL_DIR)/sbin/getcap    $(1)/usr/sbin/
	$(CP) $(PKG_INSTALL_DIR)/sbin/getpcaps  $(1)/usr/sbin/
	$(CP) $(PKG_INSTALL_DIR)/sbin/setcap    $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,libcap))
$(eval $(call BuildPackage,libcap-bin))
