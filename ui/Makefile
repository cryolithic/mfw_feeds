include $(TOPDIR)/rules.mk

PKG_NAME:=ui
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=David Wilson <dwilson@untangle.com>
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:untangle/mfw_ui.git

include ../version.mk

include $(INCLUDE_DIR)/package.mk

define Package/ui
  SECTION:=ui
  CATEGORY:=User Interface
  TITLE:=MFW new admin interface
  URL:=https://github.com/untangle/mfw_ui
  PKG_BUILD_DEPENDS:=wget node/host node-yarn/host
endef

define Package/ui/description
  MFW new admin interface
endef

define Build/Compile
	true
endef

define Package/ui/install
	# FIXME: because this build *really* *insists* on creating
	# .config/postcssrc in make's TOPDIR, and nowhere else. No
	# environment variable will convince it otherwise. We yield
	# and temporarily move openvwrt's main .config file out of the
	# way before restoring it
	mv $(TOPDIR)/.config $(TOPDIR)/.config.bak ; \
	make -C $(PKG_BUILD_DIR) DESTDIR=$(1)/www/admin install ; \
	rm -fr $(TOPDIR)/.config ; \
	mv $(TOPDIR)/.config.bak $(TOPDIR)/.config
endef

$(eval $(call BuildPackage,ui))
