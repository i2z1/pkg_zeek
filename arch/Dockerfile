
FROM ghcr.io/archlinux/archlinux:latest

ENV target zeek

RUN pacman -Syu --noconfirm && pacman -S git cmake bison flex zlib libpcap openssl-1.0 bash python swig ruby perl crypto++ libmaxmindb --noconfirm
RUN useradd -m arch
USER arch
WORKDIR /home/arch
RUN git clone -b main https://github.com/i2z1/pkg_zeek

WORKDIR /home/arch/pkg_zeek

RUN makepkg

RUN sha256sum pkg_zeek-*-x86_64.pkg.tar.zst > pkg_zeek.sha256sum
