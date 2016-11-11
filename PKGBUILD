pkgname=cenon
pkgver=4.0.2
_libver=4.0.0
pkgrel=2
pkgdesc="GNUstep vector editor for EPS, DXF, Gerber, HPGL.  Includes docs and examples."
arch=('i686' 'x86_64')
url="http://www.cenon.info"
license=('custom:vhfPL')
depends=('gnustep-base' 'gnustep-gui')
makedepends=('gnustep-make' 'gcc-objc')
options=('!strip')
source=("http://www.cenon.zone/download/source/Cenon-$pkgver.tar.bz2"
  "http://www.cenon.zone/download/source/CenonLibrary-$_libver-1.tar.bz2"
  "http://www.cenon.zone/download/doc/Cenon-4.0_gb.pdf"
  gcc47.patch)
md5sums=('ba6519d09106a250cbec72b28f970bbc'
         '5d7542f054b4ac3eb630c360d3752aa8'
         'SKIP'
         '015e2c1538788eb42c1320353a2da6e5')

prepare() {
  cd "$srcdir/Cenon"
  patch -p1 VHFShared/vhfCompatibility.h "$srcdir/gcc47.patch"

  sed -i 's|Diff((VFloat)|Diff((float)|' TileScrollView.m
  sed -i 's|(VFloat)\[\[resPopupListButton|[[resPopupListButton|' TileScrollView.m
  sed -i 's|\[\[resPopupListButton|[(TileScrollView*)[resPopupListButton|' TileScrollView.m
}

build() {
  cd "$srcdir/Cenon"

  export CFLAGS="$CFLAGS -g"
  export CXXFLAGS="$CXXFLAGS -g"

  make
}

package() {
  cd "$srcdir/Cenon"
  install -d "$pkgdir/usr/lib/GNUstep/Libraries/"
  #install -d "$pkgdir/usr/share/"
  # TODO: symlink to .desktop file
  #install -d "$pkgdir/usr/share/applications/"
  # TODO: symlink to documentation
  #install -d "$pkgdir/usr/share/doc/cenon/"

  make DESTDIR="$pkgdir" install

  # TODO: prefer install over cp
  cp -R Devices/ "$pkgdir/usr/lib/GNUstep/Cenon/"
  cp -R Examples/ "$pkgdir/usr/lib/GNUstep/Cenon/"
  cp -R Projects/ "$pkgdir/usr/lib/GNUstep/Cenon/"
  cp -R Documentation/ "$pkgdir/usr/lib/GNUstep/Cenon/"
  install ../../Cenon-4.0_gb.pdf "$pkgdir/usr/lib/GNUstep/Cenon/Documentation/"

  # figure out how to fix the library path for real
  #touch "$pkgdir/usr/bin/cenon"
  #chmod +x "$pkgdir/usr/bin/cenon"
  #echo "#!/bin/sh" >> "$pkgdir/usr/bin/cenon"
  #echo "LD_LIBRARY_PATH=\"/usr/lib/GNUstep/Libraries\" Cenon" >> "$pkgdir/usr/bin/cenon"
}



