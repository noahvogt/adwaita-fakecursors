# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=adwaita-icon-theme
pkgver=3.15.92
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
sha256sums=('06c61f1c96b5f6cac5468d79e1758493de73118bb7c1c107e2e8e5aac3b39021')

build() {
    cd "$pkgname-$pkgver"
    ./configure --prefix=/usr
    make
}

package() {
    cd "$pkgname-$pkgver"
    make DESTDIR="$pkgdir" install
}
