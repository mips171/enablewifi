#
# Copyright (C) 2006-2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=enable-wifi
PKG_RELEASE:=1

PKG_MAINTAINER:=Nicholas Smith <nicholas@nbembedded.com>
PKG_LICENSE:=GPL-3.0-or-later

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
  An optional encryption/password setting is available.
endef

define Build/Compile

ifdef WIFI_SSID
	echo "set wireless.@wifi-iface[0].ssid='"$(WIFI_SSID)"'" >> contents
endif

ifdef WIFI_ENCRYPTION
	echo "set wireless.@wifi-iface[0].encryption='"$(WIFI_ENCRYPTION)"'" >> contents
endif

ifdef WIFI_KEY
	echo "set wireless.@wifi-iface[0].key='"$(WIFI_KEY)"'" >> contents
endif

endef

define Package/enable-wifi/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/enablewifi.config $(1)/etc/uci-defaults/99999_enablewifi
endef

$(eval $(call BuildPackage,enable-wifi))
