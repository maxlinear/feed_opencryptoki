#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=opencryptoki
PKG_VERSION:=1.0.26
PKG_RELEASE:=1
PKG_SOURCE_PROTO:=git
 
PKG_PROJECT:=maxlinear
PKG_SOURCE_NAME:=opencryptoki
CONFIG_UGW_PKG_SOURCE_URL:=ssh://git@github.com
PKG_SOURCE_URL:=$(CONFIG_UGW_PKG_SOURCE_URL)/$(PKG_PROJECT)/$(PKG_NAME).git
PKG_MIRROR_HASH:=ce0ee88586068f62b3ec5f2dff93a78bddc83a156a634f62e98f9197f99e2cad
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.xz
PKG_MAINTAINER:=MaxLinear
PKG_LICENSE:=GPL-2.0

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/opencryptoki
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=A package for opencryptoki
  DEPENDS:=+libopenssl +libcap +libopenldap +sse_fapi_lgm +liboptee-client
endef

define Package/opencryptoki/description
 A tool for managing tokens
endef

CONFIGURE_VARS+= \
	CC_FOR_BUILD=gcc

CONFIGURE_ARGS+=\
        --enable-ccatok=no \
        --enable-ep11tok=no \
        --enable-icsftok=no \
        --enable-tpmtok=no \
        --enable-swtok=no \
        --enable-debug \
        --enable-pkcshsm_mk_change=no \
        --enable-pkcstok_admin=no \
        --enable-pkcstok_migrate=no \
        --enable-pkcsstats=no \
        --with-pkcsslotd-user=root \
        --with-pkcs-group=root \

define Package/opencryptoki/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) \
	$(PKG_INSTALL_DIR)/usr/sbin/pkcs* $(1)/usr/sbin/ \

	$(INSTALL_DIR) $(1)/usr/lib ;\
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/opencryptoki/*.so $(1)/usr/lib/ ;\
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/opencryptoki/libopencryptoki.so.0.0.0 $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkcs11/stdll/* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/p11sak $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/opencryptoki
	$(CP) $(PKG_INSTALL_DIR)/etc/opencryptoki/* $(1)/etc/opencryptoki/
	chmod 640 $(1)/etc/opencryptoki/*
	$(CP) ./config/providers.cnf  $(1)/etc/
	$(CP) ./config/engines.cnf $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(CP) ./files/pkcs11.init  $(1)/etc/init.d/pkcs11
endef

$(eval $(call BuildPackage,opencryptoki))
