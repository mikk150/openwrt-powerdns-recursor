#
# Copyright (C) 2015 OpenWrt-dist
#
# This is free software, licensed under the MIT.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pdns-recursor
PKG_VERSION:=4.1.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://downloads.powerdns.com/releases/
PKG_MD5SUM:=bd974f85944baa67338998d33bcd6120

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=clowwindy <clowwindy42@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/pdns-recursor
	SECTION:=net
	CATEGORY:=Network
	TITLE:=PowerDNS-Recursor
	URL:=https://github.com/PowerDNS/pdns
	DEPENDS:= +boost +lua +libopenssl
endef

define Package/pdns-recursor/description
	powerdns-recursor is a versatile high performance recursing nameserver.
endef

define Package/pdns-recursor/conffiles
	/etc/powerdns/recursor.conf
	/etc/powerdns/forward.conf
endef

define Package/pdns-recursor/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/powerdns
	$(INSTALL_BIN) ./files/pdns-recursor.init $(1)/etc/init.d/pdns-recursor
	$(INSTALL_CONF) ./files/recursor.conf $(1)/etc/powerdns/recursor.conf
	$(INSTALL_CONF) ./files/forward.conf $(1)/etc/powerdns/forward.conf
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pdns_recursor $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rec_control $(1)/usr/sbin
endef

$(eval $(call BuildPackage,pdns-recursor))
