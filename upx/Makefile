#
# Copyright (C) 2011-2022 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=upx
PKG_VERSION:=4.0.2
PKG_RELEASE:=1

PKG_MAINTAINER:=Xingwang Liao <kuoruan@gmail.com>
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_SOURCE_URL:=https://github.com/upx/upx/releases/download/v$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-src.tar.xz
PKG_HASH:=1221e725b1a89e06739df27fae394d6bc88aedbe12f137c630ec772522cbc76f
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

HOST_BUILD_DEPENDS:=ucl/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Host/Compile
	UPX_UCLDIR=$(STAGING_DIR_HOST) \
	$(MAKE) -C $(HOST_BUILD_DIR)/src \
		CXXFLAGS_WERROR="" LDFLAGS="$(HOST_LDFLAGS)" \
		CXX="$(HOSTCXX)"
endef

define Host/Install
	$(CP) $(HOST_BUILD_DIR)/src/upx.out $(STAGING_DIR_HOST)/bin/upx
endef

define Host/Clean
	rm -f $(STAGING_DIR_HOST)/bin/upx
endef

define Package/upx
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libucl +libstdcpp +zlib
  TITLE:=The Ultimate Packer for eXecutables
  URL:=https://upx.github.io/
endef

define Package/upx/description
UPX is a free, portable, extendable, high-performance executable packer for
several different executable formats. It achieves an excellent compression ratio
and offers very fast decompression. Your executables suffer no memory overhead
or other drawbacks for most of the formats supported, because of in-place
decompression.
endef

MAKE_PATH := src

define Package/upx/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/upx.out $(1)/usr/bin/upx
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,upx))
