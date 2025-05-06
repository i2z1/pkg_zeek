pkgname=zeek
pkgver=v8.0.0.dev
pkgrel=1
epoch=1
pkgdesc='A network analysis framework '
arch=('x86_64')
url='https://github.com/zeek/zeek'
license=('BSD')
depends=('libpcap' 'openssl-1.1' 'bash' 'python' 'swig' 'ruby' 'perl'
         'crypto++')
makedepends=('git' 'cmake' 'python' 'swig' 'bison' 'flex' 'zlib')
source=("git+https://github.com/$pkgname/$pkgname.git")
sha512sums=('SKIP')

pkgver() {
  cd $pkgname

  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd $pkgname

  git submodule update --init --recursive
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
