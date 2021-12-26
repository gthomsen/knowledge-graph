Tags: #linux #macos #openssl

# How Was It Built?
Determine if a particular feature was compiled in:
```shell
$ openssl version -f
compiler: /usr/bin/clang -I. -I.. -I../include  -fPIC -fno-common -DOPENSSL_PIC -DZLIB -DOPENSSL_THREADS -D_REENTRANT -DDSO_DLFCN -DHAVE_DLFCN_H -arch x86_64 -O3 -DL_ENDIAN -Wall -DOPENSSL_IA32_SSE2 -DOPENSSL_BN_ASM_MONT -DOPENSSL_BN_ASM_MONT5 -DOPENSSL_BN_ASM_GF2m -DSHA1_ASM -DSHA256_ASM -DSHA512_ASM -DMD5_ASM -DAES_ASM -DVPAES_ASM -DBSAES_ASM -DWHIRLPOOL_ASM -DGHASH_ASM -DECP_NISTZ256_ASM
```

# Listing Supported Ciphers
This is useful when troubleshooting access to systems using older ciphers as modern browsers don't tell you they aren't supporting a cipher, but present a cryptic "things broke" message for the end user to interpret.

Determine which version of SSL/TLS was compiled in:
```shell
$ openssl s_client -help 2>&1 >/dev/null | egrep "\-(ssl|tls)[^a-z]"
 -ssl2         - just use SSLv2
 -ssl3         - just use SSLv3
 -tls1_2       - just use TLSv1.2
 -tls1_1       - just use TLSv1.1
 -tls1         - just use TLSv1
```

This solution ***DOES NOT WORK*** (compare to the above from the same system):

```shell
$ openssl ciphers -v | awk '{ print $2 }' | sort | uniq
SSLv3
TLSv1.2
```