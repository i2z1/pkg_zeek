
FROM ghcr.io/archlinux/archlinux:latest

ENV target zeek

RUN pacman -Syu --noconfirm && pacman -S gcc13 git cmake bison flex zlib libpcap bash python swig ruby perl crypto++ libmaxminddb openssl jq dnsmasq --noconfirm
RUN useradd -m arch
USER arch
WORKDIR /home/arch
RUN git clone -b main https://github.com/i2z1/pkg_zeek

WORKDIR /home/arch/pkg_zeek

RUN makepkg

RUN sha256sum zeek-*-x86_64.pkg.tar.zst > zeek.sha256sum
