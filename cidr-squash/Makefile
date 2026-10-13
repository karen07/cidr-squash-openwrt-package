include $(TOPDIR)/rules.mk

PKG_NAME:=cidr-squash
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

# Local sources are located next to the *-openwrt-package repository.
PKG_LOCAL_SOURCE_DIR:=$(abspath $(realpath $(CURDIR))/../../$(PKG_NAME))

ifeq ($(wildcard $(PKG_LOCAL_SOURCE_DIR)/CMakeLists.txt),)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/karen07/cidr-squash
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip
endif

PKG_LICENSE:=AGPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Karen Khachatryan <karen0734@gmail.com>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cidr-squash
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=
  TITLE:=IPv4 CIDR optimizer
  URL:=https://github.com/karen07/cidr-squash
endef

define Package/cidr-squash/description
  IPv4 CIDR optimizer with configurable bounded over-coverage.
endef

ifneq ($(wildcard $(PKG_LOCAL_SOURCE_DIR)/CMakeLists.txt),)
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(PKG_LOCAL_SOURCE_DIR)/. $(PKG_BUILD_DIR)/
endef
endif

define Package/cidr-squash/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cidr-squash $(1)/usr/bin/cidr-squash
endef

$(eval $(call BuildPackage,cidr-squash))
