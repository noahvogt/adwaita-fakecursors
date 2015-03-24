# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=adwaita-icon-theme
pkgver=3.16.0
pkgrel=1
pkgdesc="Adwaita icon theme"
arch=(any)
depends=('hicolor-icon-theme' 'gtk-update-icon-cache')
makedepends=('intltool' 'icon-naming-utils')
url="http://www.gnome.org"
license=('GPL')
groups=('gnome')
install=adwaita-icon-theme.install
options=('!emptydirs')
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgname/${pkgver:0:4}/$pkgname-$pkgver.tar.xz)
sha256sums=('a3c8ad3b099ca571b423811a20ee9a7a43498cfa04d299719ee43cd7af6f6eb1')

build() {
    cd "$pkgname-$pkgver"
    ./configure --prefix=/usr
    make
}

package() {
    cd "$pkgname-$pkgver"
    make DESTDIR="$pkgdir" install
}
