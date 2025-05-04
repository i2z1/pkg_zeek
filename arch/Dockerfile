
FROM ghcr.io/archlinux/archlinux:latest

ENV target zeek

RUN pacman -Syu --noconfirm && pacman -S base-devel gcc glibc git cmake swig bison flex zlib libpcap make openssl geoip libmaxminddb python gperftools shadow bind-tools --noconfirm
RUN useradd -m arch
USER arch
WORKDIR /home/arch
RUN git clone -b main https://github.com/i2z1/pkg_zeek

WORKDIR /home/arch/pkg_zeek

RUN makepkg

RUN sha256sum pkg_zeek-*-x86_64.pkg.tar.zst > pkg_zeek.sha256sum
