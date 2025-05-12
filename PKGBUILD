pkgname=zeek
pkgver=v8.0.0.dev
pkgrel=1
epoch=1
pkgdesc='A network analysis framework '
arch=('x86_64')
url='https://github.com/zeek/zeek'
license=('BSD')
depends=('libpcap' 'openssl' 'bash' 'python' 'swig' 'ruby' 'perl'
         'crypto++')
makedepends=('git' 'cmake' 'python' 'swig' 'bison' 'flex' 'zlib')
source=("git+https://github.com/$pkgname/$pkgname.git"
        zeek.tmpfiles.conf)

sha256sums=('SKIP'
            'af5b7e14caae88122d0e6dd29539ae77ed3388c70a12ea0ed73c9a3f6de16d91')

#pkgver() {
#  cd $pkgname

# git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
#}

prepare() {
 cd $pkgname
 git submodule update --init --recursive
}

build() {

  cmake -B build -S "zeek" \
    -D CMAKE_CXX_COMPILER=/usr/bin/gcc-13 \ 
    -D CMAKE_INSTALL_PREFIX=/usr \
    -D ZEEK_PYTHON_PREFIX:PATH=/usr \
    -D ZEEK_ETC_INSTALL_DIR:PATH=/etc \
    -D ZEEK_STATE_DIR:PATH=/var/lib \
    -D ZEEK_SPOOL_DIR:PATH=/var/spool \
    -D ZEEK_LOG_DIR:PATH=/var/log/zeek \
    -D BINARY_PACKAGING_MODE=ON \
    -D BUILD_SHARED_LIBS=ON \
    -D BUILD_STATIC_BINPAC=ON \
    -D BROKER_DISABLE_TESTS=ON \
    -D BROKER_DISABLE_DOC_EXAMPLES=ON \
    -D INSTALL_AUX_TOOLS=ON \
    -D INSTALL_ZEEK_ARCHIVER=ON \
    -D INSTALL_ZKG=ON

  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build

  #rm -rf "$pkgdir/usr/var"

  install -dm0755 "$pkgdir/var/lib/zkg"

  install -Dm0644 zeek.tmpfiles.conf "$pkgdir/usr/lib/tmpfiles.d/zeek.conf"

 # install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname" \
 #   "zeek-$pkgver"/COPYING{,-3rdparty}
}
