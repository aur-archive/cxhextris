# Maintainer: Anton Bazhenov <anton.bazhenov at gmail>

pkgname=cxhextris
pkgver=1.0
pkgrel=1
pkgdesc="An XTetris-like game with hexagons instead of squares (color version)"
arch=('i686')
url="http://www.happypenguin.org/show?CXHextris"
license=('custom')
depends=('libxext')
makedepends=('imake' 'xorg-font-utils')
install="${pkgname}.install"
source=("http://ftp.sunet.se/pub/Linux/funet/xtra/games/x11/action/${pkgname}.tar.z"
        "00-install-paths.patch"
        "01-setfontpath.patch"
        "${pkgname}.png"
        "${pkgname}.desktop")
md5sums=('64fce30ebb859bcce0ff4f91f4ece0a8'
         'e19d1aefa49bf3edc2d465d5d95d7a7b'
         'ee0c5a86a1c39d3adc6fa1de9e1f2f7a'
         'c0a6d2e468a65ee74f156b809490067e'
         '704cd8d5b24b72509439b01efd788360')

build() {
  cd "${srcdir}/${pkgname}"

  # Apply patches
  patch -Np1 -i ../00-install-paths.patch
  patch -Np1 -i ../01-setfontpath.patch

  xmkmf
  make
}

package() {
  cd "${srcdir}/${pkgname}"

  # Install game files
  install -Dm755 xhextris "${pkgdir}/usr/bin/xhextris"
  install -Dm644 hex20.pcf "${pkgdir}/usr/share/fonts/misc/hex20.pcf"
  install -Dm664 -g games xhextris-scores "${pkgdir}/var/lib/${pkgname}/xhextris-scores"

  # Install a desktop entry
  install -Dm644 ../${pkgname}.png "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
  install -Dm644 ../${pkgname}.desktop "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  # Install a license file and man page
  sed -n "1,22p" README > COPYING
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
  install -Dm644 xhextris.man "${pkgdir}/usr/share/man/man6/xhextris.6"
}
