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
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu' 'nerd-fonts-source-code-pro' 'scrot')
install=dwm.install

_patches=(
        "dwm-systray-20190208-cb3f58a.diff"
        "dwm-noborder-20170207-bb3bd6f.diff"
        "dwm-attachaside-20180126-db22360.diff"
        "dwm-autostart-20161205-bb3bd6f.diff"
        "dwm-cyclelayouts-20180524-6.2.diff"
        "dwm-gridmode-20170909-ceac8c9.diff"
        "dwm-r1615-selfrestart.diff"
        "local-hide_vacant_tags-git-20160626-7af4d43.diff"
        "local-statuscolors-20181008-b69c870.diff"
        "local-fancybar-2019018-b69c870.diff"
        "local-scratchpad-20170207-bb3bd6f.diff"
#        "local-notitle-6.2.diff"
        "local-alpha-20180613-b69c870.diff"
        )

source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
    config.h
    dwm.desktop
    "${_patches[@]}")

md5sums=('9929845ccdec4d2cc191f16210dd7f3d'
         '456a3571a825fdddfd61bfc2d3f9e1e9'
         '939f403a71b6e85261d09fc3412269ee'
         '31a7569d7f3d43846f59e854ec5d1da0'
         'fbb786263f2d714b18368ff64779d669'
         'c75af619c04cfae7b9740ec140d1dc6c'
         '46ff022e2a2c6139e71399eb19d1aebb'
         '5baffd8c124095d06b133e9b31a854b2'
         '6055775113fd4dc06200bc6aaafb72fb'
         'aa3d5f3c45057a2a6ee73aede3fc218a'
         'd2781ac29048fc50e42e0f11e6cf7bce'
         'c5469c1457955a8447e05ec5118b3ce6'
         '77e3bfab2270dde73caf4e1b14566386'
         '7381051e12596394791092f0d39a2dd2'
         '60a545c6661638af619913e2a093ebf8')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  sed -i "25 a \ \t{ NULL,       NULL }," "$srcdir/$(basename ${_patches[5]})"

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
