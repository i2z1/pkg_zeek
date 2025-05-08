pkgname=zeek
pkgver=v8.0.0.dev.r59.g6f8924596
pkgrel=1
epoch=1
pkgdesc='A network analysis framework '
arch=('x86_64')
url='https://github.com/zeek/zeek'
license=('BSD')
depends=('libpcap' 'openssl-1.1' 'bash' 'python' 'swig' 'ruby' 'perl'
         'crypto++')
makedepends=('git' 'cmake' 'python' 'swig' 'bison' 'flex' 'zlib')
source=("git+https://github.com/$pkgname/$pkgname.git"
        spicy_hilti.patch
        zeek.patch)
sha256sums=('SKIP'
            'd4e80c3a799e70676423dcab80944d89a8e0d564ba8cd0a4c8091a2b762ee8f0'
            '31ca5535356204c8aaf400ea5c267b5655b469a5424b06cb4793b5d2f6a9700b')

pkgver() {
  cd $pkgname

  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd $pkgname
  git submodule update --init --recursive

  cp ../"zeek.patch" $srcdir/zeek/
  cd $srcdir/zeek/
  git apply "zeek.patch"

  cp ../spicy_hilti.patch $srcdir/zeek/auxil/spicy/
  cd $srcdir/zeek/auxil/spicy/
  git apply "spicy_hilti.patch"

}

build() {
  cd $pkgname

  ./configure \
    --prefix=/usr/share/zeek \
    --disable-broker-tests \
    --disable-cpp-tests \

  make
}

package() {
  cd $pkgname

  install -dm 755 "$pkgdir/usr/bin"

  make DESTDIR="$pkgdir" install

  install -Dm 644 -t "$pkgdir/usr/share/doc/$pkgname" README CHANGES VERSION
  install -Dm 644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"

  cp -a "$pkgdir/usr/share/$pkgname/bin/"* "$pkgdir/usr/bin/"
  rm -rf "$pkgdir/usr/share/$pkgname/bin"
}
