# $Id$
# Maintainer: Ryan Kes <ryan@ryankes.eu>

pkgname=higherlearning-dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'dmenu' 'ttf-jetbrains-mono' 'ttf-joypixels')
optdepends=('gllock-git' 'higherlearning-st')
conflicts=('dwm')
install=dwm.install

_patches=(
        "dwm-noborder-6.2.diff"
        "dwm-autostart-20200610-cb3f58a.diff"
        "dwm-cyclelayouts-20180524-6.2.diff"
        "local-gridmode-20170909-ceac8c9.diff"
        "local-r1615-selfrestart.diff"
        "dwm-hide_vacant_tags-6.2.diff"
        "local-scratchpad-6.2.diff"
        "dwm-rotatestack-20161021-ab9571b.diff"
        "dwm-statuspadding-20150524-c8e9479.diff"
        "local-uselessgap-6.2.diff"
        "local-allow-color-fonts.diff"
        "dwm-alpha-20201019-61bb8b2.diff"
        )

source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
    config.h
    dwm.desktop
    "${_patches[@]}")

md5sums=('9929845ccdec4d2cc191f16210dd7f3d'
         '418abafd90ec84255144dcea538a53fb'
         '939f403a71b6e85261d09fc3412269ee'
         '453062a348098b240e55f40623f14ed0'
         '64cc9cc8df63451b660a76c31ca67a34'
         '5baffd8c124095d06b133e9b31a854b2'
         '272fdc4d250d3c30750dbe56bb7e9fa5'
         '8c3ad89cb98dd2b9152075b6e29cb579'
         'c446b71a8b8cce25db86a47805500dfa'
         '595df893d829b2994bb799d12a1c9545'
         '882e0783ccedf9fbb8b565e7681116c9'
         'd1f932d25d82eb9aaa589a54d9b4e6c8'
         'b9c840237160440110fdafc204eff208'
         'cdf4c9dacfecd8f3aecb5fc8166c4604'
         '7799f60a9e87e4f99e813d158abee15b')

prepare() {
  cd $srcdir/dwm-$pkgver
  #sed -i "25 a \ \t{ NULL,       NULL }," "$srcdir/$(basename ${_patches[4]})"

  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/dwm-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/dwm-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/dwm/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/dwm/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
