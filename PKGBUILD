# Maintainer: Marq Schneider <queueRAM@gmail.com>

pkgname=kicad
pkgver=20120119.bzr3256
pkgrel=1
pkgdesc="Electronic schematic and printed circuit board (PCB) design tools"
arch=('i686' 'x86_64')
url="http://iut-tice.ujf-grenoble.fr/kicad/"
license=('GPL')
depends=('mesa' 'shared-mime-info' 'wxgtk')
makedepends=('boost' 'cmake' 'zlib')
optdepends=('kicad-doc-bzr' 'kicad-library-bzr')
install=kicad.install
source=(http://iut-tice.ujf-grenoble.fr/cao/${pkgname}_sources-${pkgver:0:4}-${pkgver:4:2}-${pkgver:6:2}-BZR${pkgver:12:4}-stable.zip
        kicad-boost-polygon-declare-gtlsort-earlier.patch)
md5sums=('d65574c42efd72638aed80adef367c3b'
         'a2c39704238946e74a5ed0c38326345f')

build() {
  cd ${srcdir}/KiCad_sources

  patch -p0 < ${srcdir}/kicad-boost-polygon-declare-gtlsort-earlier.patch

  # build and install kicad
  mkdir -p build/Release && cd build/Release
  cmake ../.. -DKICAD_STABLE_VERSION=ON    \
              -DCMAKE_BUILD_TYPE=Release   \
              -DCMAKE_INSTALL_PREFIX=/usr
  make
}

package() {
  cd ${srcdir}/KiCad_sources/build/Release

  make DESTDIR=${pkgdir} install

  # copy updated linux icons
  #cp -r -n ${srcdir}/${pkgname}-icons/resources/linux/mime/icons ${pkgdir}/usr/share/
}
