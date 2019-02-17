# $Id$
# Maintainer: Ryan Kes <alrayyes@gmail.com> 

pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu' 'nerd-fonts-source-code-pro')
install=dwm.install

_patches=(
        "https://dwm.suckless.org/patches/systray/dwm-systray-20180314-3bd8466.diff"
        "https://dwm.suckless.org/patches/noborder/dwm-noborder-20170207-bb3bd6f.diff"
        "https://dwm.suckless.org/patches/attachaside/dwm-attachaside-20180126-db22360.diff"
        )

source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
	dwm.desktop
	"${_patches[@]}")

md5sums=('9929845ccdec4d2cc191f16210dd7f3d'
         '8c46375a39600b69954298febfdff020'
         '939f403a71b6e85261d09fc3412269ee'
         '2c19f1a3db59e158c45483668f4cee24'
         'fbb786263f2d714b18368ff64779d669'
         'c75af619c04cfae7b9740ec140d1dc6c')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  
  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
