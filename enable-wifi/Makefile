#
# Copyright (C) 2006-2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=enable-wifi
PKG_VERSION:=0.1
PKG_RELEASE:=1

PKG_MAINTAINER:=Nicholas Smith <nicholas@nbembedded.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/enable-wifi/config
  source "$(SOURCE)/Config.in"
endef

define Package/enable-wifi
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Enable wireless radios on first boot
  URL:=https://github.com/openwrt/packages/net/enable-wifi
endef

define Package/enable-wifi/description
  This is a simple UCI-defaults script that enables the wifi on the first boot.
  An optionial encryption/password setting is available.
endef

ifdef SSID
  echo "set wireless.@wifi-iface[0].ssid='"$(SSID)"'" >> contents
endif

ifdef ENCRYPTION
  echo "set wireless.@wifi-iface[0].encryption='"$(ENCRYPTION)"'" >> contents
endif

ifdef KEY
  echo "set wireless.@wifi-iface[0].key='"$(KEY)"'" >> contents
endif

define Package/enable-wifi/install
  $(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/enablewifi.config $(1)/etc/uci-defaults/99999_enablewifi
endef

$(eval $(call BuildPackage,enable-wifi))
