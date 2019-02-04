# $Id$
# Maintainer: Ryan Kes <alrayyes@gmail.com> 

pkgname=dwm
pkgver=6.1
pkgrel=3
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu' 'nerd-fonts-source-code-pro')
install=dwm.install

_patches=("https://dwm.suckless.org/patches/alpha/dwm-alpha-6.1.diff"
        "https://dwm.suckless.org/patches/activetagindicatorbar/dwm-activetagindicatorbar-6.1.diff"
        "https://dwm.suckless.org/patches/noborder/dwm-noborder-6.1.diff")

source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
	dwm.desktop
	"${_patches[@]}")

md5sums=('f0b6b1093b7207f89c2a90b848c008ec'
         'e1a6e5202ef2c9a0d338a63f9464b656'
         '939f403a71b6e85261d09fc3412269ee'
         'e6858ff16b9eb1d7fa42a96b59847395'
         '4c0b9919df89804a4b344c1405757019'
         '7e25b6da25308c899d2ac6eb322cc69d')

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
