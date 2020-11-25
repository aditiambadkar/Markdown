# USBGuard

## Table of Contents

### 1. [About](#about)

### 2. [Installation](#installation)

### 3. [Starting USBGuard](#starting-usbguard)

## About

The [USBGuard](https://usbguard.github.io/) software framework helps to protect your computer against rogue USB devices (a.k.a. [BadUSB](https://opensource.srlabs.de/projects/badusb)) by implementing basic whitelisting and blacklisting capabilities based on device attributes.

## Installation


1. Download the release tarball [usbguard-0.7.2.tar.gz](https://github.com/USBGuard/usbguard/releases/tag/usbguard-0.7.2). This is the compatible version for Ubuntu 18.04.
2. Extract the tarball:

`$ tar -xf usbguard-0.7.2.tar.gz`

3. Install the dependencies:

`$ sudo apt install ibsodium-dev protobuf-compiler libprotobuf-dev libdbus-1-dev libdbus-glib-1-dev libpolkit-gobject-1-dev asciidoctor`

4. Configure USBGuard:

```
$ cd usbguard-0.7.2
$ ./configure --prefix=/usr --sysconfdir=/etc --with-bundled-catch --with-bundled-pegtl --with-crypto-library=sodium --enable-systemd\
$ make
$ sudo make install
$ sudo ldconfig
```

## Starting USBGuard

1. Generate an initial policy:

```
$ sudo usbguard generate-policy > rules.conf
$ sudo install -m 0600 -o root -g root rules.conf /etc/usbguard/rules.conf
```

2. Start USBGuard:

```
$ sudo systemctl start usbguard
```

3. Check the USBGuard Status:

```
$ sudo systemctl status usbguard
● usbguard.service - USBGuard daemon
   Loaded: loaded (/lib/systemd/system/usbguard.service; disabled; vendor preset: enabled)
   Active: active (running) since Wed 2020-11-25 09:42:14 +04; 2h 49min ago
     Docs: man:usbguard-daemon(8)
  Process: 26137 ExecStart=/usr/sbin/usbguard-daemon -f -s -c /etc/usbguard/usbguard-daemon.conf (code=exited, status=0/SUCCESS)
 Main PID: 26139 (usbguard-daemon)
    Tasks: 3 (limit: 4915)
   CGroup: /system.slice/usbguard.service
           └─26139 /usr/sbin/usbguard-daemon -f -s -c /etc/usbguard/usbguard-daemon.conf
```
