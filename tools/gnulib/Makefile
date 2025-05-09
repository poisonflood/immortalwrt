include $(TOPDIR)/rules.mk

PKG_NAME:=gnulib
PKG_CPE_ID:=cpe:/a:gnu:$(PKG_NAME)
PKG_VERSION:=dfc9412e98c0c527fed3c71af3a03b0e91f53620# # master@250510 commit_hash# tag_hash#

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.savannah.gnu.org/cgit/$(PKG_NAME).git/snapshot
PKG_HASH:=a59d8358ac06789d8d51723e1eab5ea74e7538ae54f87d12d778cb9bfc6c2f9f

include $(INCLUDE_DIR)/host-build.mk

define Host/Configure
endef

define Host/Install
	$(INSTALL_DIR) $(1)/share/aclocal
	$(INSTALL_DATA) $(HOST_BUILD_DIR)/m4/*.m4 $(1)/share/aclocal/
	$(INSTALL_DIR) $(1)/share/gnulib
	$(CP) $(HOST_BUILD_DIR)/{*,.*} $(1)/share/gnulib/
	ln -sf ../share/gnulib/gnulib-tool $(STAGING_DIR_HOST)/bin/gnulib-tool
endef

define Host/Clean
	rm -rf $(STAGING_DIR_HOST)/bin/gnulib-tool $(STAGING_DIR_HOST)/share/gnulib
endef

$(eval $(call HostBuild))
