# Using OpenSSL as Crypto Library for USBGuard

## Table of Contents

### 1. [About OpenSSL](#about-openssl)

### 2. [Install Dependencies](#install-dependencies)

### 3. [Modifications in USBGuard Source Files](#modifications-in-usbguard-source-files)

### 4. [Install USBGuard](#install-usbguard)

### 5. [References](#references)

## About OpenSSL

[OpenSSL](https://www.openssl.org/) is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library.

## Install Dependencies

```$ sudo apt install libtool libssl-dev```

1. Extract the tarball:

`$ tar -xf usbguard-0.7.2.tar.gz`

3. Install the dependencies:

`$ sudo apt install ibsodium-dev protobuf-compiler libprotobuf-dev libdbus-1-dev libdbus-glib-1-dev libpolkit-gobject-1-dev asciidoctor`

4. Configure USBGuard:

```
$ cd usbguard-0.7.2
$ ./configure --prefix=/usr --sysconfdir=/etc --with-bundled-catch --with-bundled-pegtl --with-crypto-library=sodium --enable-systemd
$ make
$ sudo make install
$ sudo ldconfig
```

## Modifications in USBGuard Source Files

1. configure.ac:
   a. Check for OpenSSL library.

   b. Check for --with-crypto-library=selector (add support for openssl)

2. configure:

   a. Configure OpenSSL 1.1.1

   b. Set crypto_CFLAGS="$openssl_CFLAGS" crypto_LIBS="$openssl_LIBS"

3. src/Library/Hash.hpp:

   a. Include openssl/sha.h

   b. Create SHA256_CTX object

4. src/Library/Hash.cpp:

   a. Add the OpenSSL SHA256 functions - SHA256_Init, SHA256_Update and SHA256_Final


## Install USBGuard

1. ```$ autoreconf -f -i```

2. Give openssl as parameter for --with-crypto-library:
```
$ ./configure --prefix=/usr --sysconfdir=/etc --with-bundled-catch --with-bundled-pegtl --with-crypto-library=openssl --enable-systemd
$ make
$ sudo make install
$ sudo ldconfig
```

## References

1. https://github.com/openssl/openssl/blob/master/include/openssl/sha.h
2. https://www.openssl.org/docs/man1.1.1/