include $(TOPDIR)/rules.mk

PKG_NAME:=gperf
PKG_VERSION:=3.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/gperf
PKG_HASH:=fd87e0aba7e43ae054837afd6cd4db03a3f2693deb3619085e6ed9d8d9604ad8

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

HOST_CPPFLAGS:=-I$(HOST_BUILD_DIR)/lib -I$(HOST_BUILD_DIR)/src $(HOST_CPPFLAGS)
TARGET_CPPFLAGS:=-I$(PKG_BUILD_DIR)/lib -I$(PKG_BUILD_DIR)/src $(TARGET_CPPFLAGS)

HOST_CXXFLAGS += -std=c++11

define Package/gperf
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=GNU gperf
  URL:=http://www.gnu.org/software/gperf
  DEPENDS:=+libstdcpp
endef

define Package/gperf/description
 GNU gperf is a perfect hash function generator. For a given list of strings,
 it produces a hash function and hash table, in form of C or C++ code,
 for looking up a value depending on the input string.
 The hash function is perfect, which means that the hash table has no collisions,
 and the hash table lookup needs a single string comparison only.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		CXXFLAGS="$(TARGET_CPPFLAGS)"
endef

define Package/gperf/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/gperf $(1)/usr/bin/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,gperf))
