# Contributor: Lukas Fleischer <lfleischer@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=adwaita-icon-theme
pkgver=3.24.0
pkgrel=1
pkgdesc="GNOME standard icons"
url="https://git.gnome.org/browse/adwaita-icon-theme"
arch=(any)
license=(LGPL3 CCPL:cc-by-sa)
depends=(hicolor-icon-theme gtk-update-icon-cache librsvg)
makedepends=(intltool git gtk3)
groups=(gnome)
_commit=a4fc30b28c60d1dbb40ab3e81c4eee588fb2116b  # tags/3.24.0^0
source=("git+https://git.gnome.org/browse/adwaita-icon-theme#commit=$_commit")
sha256sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgname
  autoreconf -fvi
}
  
build() {
  cd $pkgname
  ./configure --prefix=/usr
  make
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}
