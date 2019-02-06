# $Id$
# Maintainer: Ryan Kes <alrayyes@gmail.com> 

pkgname=dwm
pkgver=6.2
pkgrel=3
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu' 'nerd-fonts-source-code-pro')
install=dwm.install

_patches=("https://dwm.suckless.org/patches/alpha/dwm-alpha-20180613-b69c870.diff"
        "https://dwm.suckless.org/patches/noborder/dwm-noborder-20170207-bb3bd6f.diff")

source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
	dwm.desktop
	"${_patches[@]}")

md5sums=('9929845ccdec4d2cc191f16210dd7f3d'
         '49875b8dd04346410b570bb85c9c6f3a'
         '939f403a71b6e85261d09fc3412269ee'
         '4e5893e04c443530168223639c97bc47'
         'fbb786263f2d714b18368ff64779d669')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  
  # Update systray patch to fix conflicts
  #sed -i 's/+253,24/+254,24/g' "$srcdir/$(basename ${_patches[3]})"
  #sed -i '117 a \ static void xinitvisual();' "$srcdir/$(basename ${_patches[2]})"
  
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
