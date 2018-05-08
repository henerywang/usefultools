# strongswan VPN
## 1.1 移植
### 1.1.1 安装
Strongswan基于开源软件包strongswan-5.6.2.tar.gz，由strongswan的官方下载（https://www.strongswan.org/download.html）。目前5.6.2是最新的版本。  
* 装备  
进入mu/component/internet,添加vpn目录，把strongswan.tar.gz放到implement目录下
* 配置
vi makefile 主要完成如下功能： 
··
prepare:
        $(shell [ -d $(MUDP_BUILD_DIR)/$(RELATIVE_PATH) ] || mkdir -p $(MUDP_BUILD_DIR)/$(RELATIVE_PATH))
        tar -xzvf $(MODULE).tar.gz -C  $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)
        cd $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE);./configure CC=$(CROSS_COMPILE)gcc --enable-eap-identity --enable-eap-identity --enable-eap-md5 --enable-eap-mschapv2 --enable-eap-tls --enable-eap-ttls --enable-eap-peap --enable-eap-tnc --enable-eap-dynamic  --enable-xauth-eap   --enable-addrblock --enable-unity   --disable-gmp --host=$(TARGET)
rootfs:
        cd $(MUDP_ROOTFS_DIR) && mkdir -p usr/local/etc/ipsec.d  usr/local/etc/strongswan.d/charon  usr/local/etc/swanctl  usr/local/lib/ipsec/plugins  usr/local/libexec/ipsec usr/local/bin usr/local/sbin
        cd $(MUDP_ROOTFS_DIR)/usr/local/etc/ipsec.d && mkdir -p cacerts aacerts ocspcerts acerts crls
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/ipsec/_ipsec                                $(MUDP_ROOTFS_DIR)/usr/local/sbin/ipsec
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/charon/.libs/charon                         $(MUDP_ROOTFS_DIR)/usr/local/libexec/ipsec/charon
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/_copyright/.libs/_copyright                 $(MUDP_ROOTFS_DIR)/usr/local/libexec/ipsec/_copyright
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/scepclient/.libs/scepclient                 $(MUDP_ROOTFS_DIR)/usr/local/libexec/ipsec/scepclient
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/starter/.libs/starter                       $(MUDP_ROOTFS_DIR)/usr/local/libexec/ipsec/starter
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/stroke/.libs/stroke                         $(MUDP_ROOTFS_DIR)/usr/local/libexec/ipsec/stroke
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/_updown/_updown                             $(MUDP_ROOTFS_DIR)/usr/local/libexec/ipsec/_updown
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/.libs/libstrongswan.so.0      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/libstrongswan.so.0
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/.libs/libcharon.so.0              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/libcharon.so.0
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libpttls/.libs/libpttls.so.0                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/libpttls.so.0
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libtls/.libs/libtls.so.0                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/libtls.so.0
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libtnccs/.libs/libtnccs.so.0                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/libtnccs.so.0
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/vici/.libs/libvici.so     $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/libvici.so.0
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/addrblock/.libs/libstrongswan-addrblock.so            $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-addrblock.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/des/.libs/libstrongswan-des.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-des.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_tls/.libs/libstrongswan-eap-tls.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-tls.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pubkey/.libs/libstrongswan-pubkey.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pubkey.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/socket_default/.libs/libstrongswan-socket-default.so  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-socket-default.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/aes/.libs/libstrongswan-aes.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-aes.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/dnskey/.libs/libstrongswan-dnskey.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-dnskey.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_tnc/.libs/libstrongswan-eap-tnc.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-tnc.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pem/.libs/libstrongswan-pem.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pem.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/random/.libs/libstrongswan-random.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-random.so
         cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pem/.libs/libstrongswan-pem.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pem.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/random/.libs/libstrongswan-random.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-random.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/xauth_eap/.libs/libstrongswan-xauth-eap.so            $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-xauth-eap.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/attr/.libs/libstrongswan-attr.so                      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-attr.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/xauth_generic/.libs/libstrongswan-xauth-generic.so    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-xauth-generic.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/cmac/.libs/libstrongswan-cmac.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-cmac.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_identity/.libs/libstrongswan-eap-identity.so      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-identity.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_md5/.libs/libstrongswan-eap-md5.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-md5.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/hmac/.libs/libstrongswan-hmac.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-hmac.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/unity/.libs/libstrongswan-unity.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-unity.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/kernel_netlink/.libs/libstrongswan-kernel-netlink.so  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-kernel-netlink.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/sha1/.libs/libstrongswan-sha1.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-sha1.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/updown/.libs/libstrongswan-updown.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-updown.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/md5/.libs/libstrongswan-md5.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-md5.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/counters/.libs/libstrongswan-counters.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-counters.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_dynamic/.libs/libstrongswan-eap-dynamic.so        $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-dynamic.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_mschapv2/.libs/libstrongswan-eap-mschapv2.so      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-mschapv2.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_peap/.libs/libstrongswan-eap-peap.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-peap.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/eap_ttls/.libs/libstrongswan-eap-ttls.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-eap-ttls.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/constraints/.libs/libstrongswan-constraints.so    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-constraints.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/curve25519/.libs/libstrongswan-curve25519.so      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-curve25519.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/dnskey/.libs/libstrongswan-dnskey.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-dnskey.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/fips_prf/.libs/libstrongswan-fips-prf.so          $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-fips-prf.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/kernel_netlink/.libs/libstrongswan-kernel-netlink.so  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-kernel-netlink.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/nonce/.libs/libstrongswan-nonce.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-nonce.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pgp/.libs/libstrongswan-pgp.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pgp.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pkcs12/.libs/libstrongswan-pkcs12.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pkcs12.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pkcs1/.libs/libstrongswan-pkcs1.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pkcs1.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pkcs7/.libs/libstrongswan-pkcs7.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pkcs7.so

        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/pkcs8/.libs/libstrongswan-pkcs8.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-pkcs8.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/rc2/.libs/libstrongswan-rc2.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-rc2.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/resolve/.libs/libstrongswan-resolve.so                $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-resolve.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/revocation/.libs/libstrongswan-revocation.so      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-revocation.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/sha2/.libs/libstrongswan-sha2.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-sha2.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/sshkey/.libs/libstrongswan-sshkey.so              $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-sshkey.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/stroke/.libs/libstrongswan-stroke.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-stroke.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libtnccs/plugins/tnc_tnccs/.libs/libstrongswan-tnc-tnccs.so             $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-tnc-tnccs.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/unity/.libs/libstrongswan-unity.so                    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-unity.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/updown/.libs/libstrongswan-updown.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-updown.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/vici/.libs/libstrongswan-vici.so                      $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-vici.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/x509/.libs/libstrongswan-x509.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-x509.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/xauth_eap/.libs/libstrongswan-xauth-eap.so            $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-xauth-eap.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libcharon/plugins/xauth_generic/.libs/libstrongswan-xauth-generic.so    $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-xauth-generic.so
        cp $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/src/libstrongswan/plugins/xcbc/.libs/libstrongswan-xcbc.so                  $(MUDP_ROOTFS_DIR)/usr/local/lib/ipsec/plugins/libstrongswan-xcbc.so
        cd $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/conf/options/ && cp -f charon.conf charon-logging.conf  pki.conf scepclient.conf  starter.conf  swanctl.conf  tnc.conf $(MUDP_ROOTFS_DIR)/usr/local/etc/strongswan.d
        cp -f $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/conf/options/*.conf  $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)/conf/plugins/*.conf     $(MUDP_ROOTFS_DIR)/usr/local/etc/strongswan.d/charon

clean:
        #make -C $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE) uninstall
        $(Q)if [ -f $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE) ]; then make -C $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE) uninstall ; fi
        rm -rf $(MUDP_BUILD_DIR)/$(RELATIVE_PATH)/$(MODULE)
··


