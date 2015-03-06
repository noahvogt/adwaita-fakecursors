# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=adwaita-icon-theme
pkgver=3.15.90
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
sha256sums=('8293aa7f9937cbc7c95ab64a18dc6f89ca4fadb821bdc2c00c91878040db6789')

build() {
    cd "$pkgname-$pkgver"
    ./configure --prefix=/usr
    make
}

package() {
    cd "$pkgname-$pkgver"
    make DESTDIR="$pkgdir" install
}
