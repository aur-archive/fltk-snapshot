# Maintainer: Uroš Vampl <mobile.leecher at gmail dot com>

pkgname=fltk-snapshot
pkgver=1.3.0r9701
pkgrel=1
_ver=1.3.x-r9701
pkgdesc="Graphical user interface toolkit for X; svn snapshot, plus TigerVNC patch"
arch=('i686' 'x86_64')
license=('custom:LGPL')
url="http://www.fltk.org/"
depends=('libjpeg' 'libpng' 'libxft' 'libxinerama' 'libxcursor'
         'hicolor-icon-theme' 'desktop-file-utils' 'xdg-utils')
options=('!docs')
install=fltk.install
conflicts=('fltk')
provides=('fltk')
source=(http://ftp.funet.fi/pub/mirrors/ftp.easysw.com/pub/fltk/snapshots/fltk-$_ver.tar.bz2
        tigervnc.patch)
md5sums=('d109e5ffd77696f832b02e65ff8e2d23'
         'b3b5ffeab711463ca3af4636b6789457')

build() {
  cd "$srcdir/fltk-$_ver"
  patch -p1 -i "$srcdir/tigervnc.patch"
  autoconf --force
  ./configure --prefix=/usr --enable-shared
  make
}

package() {
  cd "$srcdir/fltk-$_ver"
  make DESTDIR="$pkgdir" install
  (cd fluid; make DESTDIR="$pkgdir" install install-linux)
  chmod 644 "$pkgdir"/usr/lib/*.a
  install -D -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
