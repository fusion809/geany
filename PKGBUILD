# $Id: PKGBUILD 175416 2016-05-15 15:31:02Z arodseth $
# Maintainer: Alexander F Rødseth <xyproto@archlinux.org>
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: Ionut Biru  <ibiru@archlinux.ro>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Allan McRae <mcrae_allan@hotmail.com>

pkgname=geany
pkgver=1.28.0
pkgrel=1
pkgdesc='Fast and lightweight IDE'
arch=('x86_64' 'i686')
url='http://www.geany.org/'
license=('GPL')
depends=('gtk2' 'hicolor-icon-theme' 'desktop-file-utils')
makedepends=('perl-xml-parser' 'intltool')
optdepends=('geany-plugins: various extra features'
            'vte: terminal support'
            'python2')
source=("git+https://github.com/geany/geany.git#tag=${pkgver}")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  git describe --tags `git rev-list --tags --max-count=1`
}

prepare() {
  cd "$pkgname"

  # Python2 fix
  sed -i '0,/on/s//on2/' data/templates/files/main.py

  # Syntax highlighting for PKGBUILD files
  sed -i 's/Sh=/Sh=*.install;*.ebuild;*.SlackBuild;/' data/filetype_extensions.conf
}

build() {
  cd "$pkgname"

  ./autogen.sh --prefix=/usr
  make
}

package() {
  make -C "$pkgname" DESTDIR="$pkgdir" install
}
