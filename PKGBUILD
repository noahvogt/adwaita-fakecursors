# Contributor: Lukas Fleischer <lfleischer@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=adwaita-icon-theme
pkgver=3.26.0
pkgrel=1
pkgdesc="GNOME standard icons"
url="https://git.gnome.org/browse/adwaita-icon-theme"
arch=(any)
license=(LGPL3 CCPL:cc-by-sa)
depends=(hicolor-icon-theme gtk-update-icon-cache librsvg)
makedepends=(intltool git gtk3 gnome-common)
groups=(gnome)
_commit=7b911bd35d445a0933994044a212b172e09feb1c  # tags/3.26.0^0
source=("git+https://git.gnome.org/browse/adwaita-icon-theme#commit=$_commit")
sha256sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgname

  # Fix up missing tag
  git tag -f 3.25.91 948a38e4d4eae2fec50a52cf7aace6b20fa053c8

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
