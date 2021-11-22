include $(TOPDIR)/rules.mk

PKG_NAME:=gost_engine
PKG_VERSION:=1.1.1g
PKG_RELEASE:=$(AUTORELEASE)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=ossl_patched
PKG_SOURCE_URL:=https://github.com/gost-engine/engine.git
PKG_MAINTAINER:=Artur Petrov <github@phpchain.ru>
PKG_LICENSE:=OpenSSL

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

PKG_INSTALL:=

ENGINES_DIR:=engines-1.1

define Package/gost_engine/Default
  TITLE:=GOST engine for OpenSSL
  URL:=http://www.openssl.org/
  SECTION:=libs
  CATEGORY:=Libraries
endef

define Package/gost_engine/Default/description
Russian GOST crypto algorithms for OpenSSL.
endef

define Package/libopenssl-gost_engine
    $(call Package/gost_engine/Default)
    SUBMENU:=SSL
    TITLE+= (library)
    URL:=https://github.com/gost-engine/engine/
    DEPENDS:=libopenssl @OPENSSL_ENGINE +libopenssl-conf
endef

define Package/libopenssl-gost_engine/description
$(call Package/gost_engine/Default/description)
This package contains the GOST engine library.

Support ciphers:
kuznyechik-cbc  (256 bit key, 128 bit block)
kuznyechik-cfb  (256 bit key, 128 bit block, TLS client/server mode only)
kuznyechik-ofb  (256 bit key, 128 bit block, TLS client/server mode only)
gost89  (256 bit key, 8 bit block, TLS client/server mode only)
gost89-cbc  (256 bit key, 64 bit block)
gost89-cnt  (256 bit key, 64 bit block, TLS client/server mode only)
gost89-cnt-12  (256 bit key, 8 bit block, TLS client/server mode only)
magma-cbc  (256 bit key, 64 bit block)

Support digests:
gost-mac 32 bit digest size
gost-mac-12 32 bit digest size
md_gost12_256 256 bit digest size
md_gost12_512 512 bit digest size
magma-mac 64 bit digest size
kuznyechik-ctr-acpkm-omac 128 bit digest size
kuznyechik-mac 128 bit digest size
endef

define Package/gost_engine-util
    $(call Package/gost_engine/Default)
    SECTION:=utils
    CATEGORY:=Utilities
    DEPENDS:=libopenssl-gost_engine
    TITLE+= (utilities)
endef

define Package/gost_engine-util/description
$(call Package/gost_engine/Default/description)
This package contains the GOST engine command-line utilities gostsum and gost12sum.
endef

CMAKE_OPTIONS += -DOPENSSL_ENGINES_DIR=/opt/lib/$(ENGINES_DIR)

define Package/libopenssl-gost_engine/install
	$(INSTALL_DIR) $(1)/opt/lib/$(ENGINES_DIR)
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/bin/gost.so \
			$(1)/opt/lib/$(ENGINES_DIR)/
endef

define Package/gost_engine-util/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/{gost12sum,gostsum} \
			$(1)/opt/bin/
endef


$(eval $(call BuildPackage,libopenssl-gost_engine))
$(eval $(call BuildPackage,gost_engine-util))
