include $(TOPDIR)/rules.mk

PKG_NAME:=trace-cmd
PKG_VERSION:=3.3.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_NAME)-v$(PKG_VERSION)
PKG_SOURCE_URL:=@KERNEL/utils/trace-cmd/trace-cmd.git
PKG_MIRROR_HASH:=911a3b3d4636de7e39f601a6edc0a3c3cf497035b982a2ee633f50c1fcebe666

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_FLAGS:=no-mips16
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/trace-cmd
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=Linux trace command line utility
  DEPENDS:=+libtracefs +zlib
endef

define Package/trace-cmd-extra
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=Extra plugins for trace-cmd
  DEPENDS:=+libtraceevent-extra
endef

MAKE_FLAGS += \
	NO_PYTHON=1 \
	NO_AUDIT=1 \
	NO_LIBZSTD=1 \
	prefix=/usr

define Package/trace-cmd/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib/traceevent/plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/trace-cmd $(1)/usr/bin/
endef

$(eval $(call BuildPackage,trace-cmd))
$(eval $(call BuildPackage,trace-cmd-extra))
