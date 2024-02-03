# Maintainer: Fabian Bornschein <fabiscafe-at-mailbox-dot-org>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Lukas Fleischer <lfleischer@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgbase=adwaita-icon-theme
pkgname=(
  adwaita-icon-theme
  adwaita-fake-cursors
)
pkgver=45.0
pkgrel=1
pkgdesc="GNOME standard icons"
url="https://gitlab.gnome.org/GNOME/adwaita-icon-theme"
arch=(any)
license=(
  CCPL:by-sa
  LGPL3
)
depends=(
  hicolor-icon-theme
  gtk-update-icon-cache
  librsvg
)
makedepends=(
  xorg-xcursorgen
  git
  gtk3
  meson
)
_commit=709725baa9e17e8d0ca62eab7920162bfeda37b9  # tags/45.0^0
source=("git+https://gitlab.gnome.org/GNOME/adwaita-icon-theme.git#commit=$_commit"
        "git+https://git.noahvogt.com/noah/transparent-xcursor.git")
b2sums=('SKIP' 'SKIP')

pkgver() {
  cd $pkgbase
  git describe --tags | sed 's/[^-]*-g/r&/;s/-/+/g'
}

prepare() {
  cd $pkgbase

  # rm unused and problematic .icon-theme.cache.
  git cherry-pick -n 32affe610606b3a550c2953993a72063eb2b7381
}

build() {
  arch-meson $pkgbase build
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package_adwaita-icon-theme() {
  depends+=(adwaita-cursors)

  meson install -C build --destdir "$pkgdir"

  mkdir -p cursors/usr/share/icons/Adwaita
  mv {"$pkgdir",cursors}/usr/share/icons/Adwaita/cursors
}

package_adwaita-fake-cursors() {
  pkgdesc="GNOME standard cursors"
  depends=()
  provides=(adwaita-cursors)
  conflicts=(adwaita-cursors)
  cd "$srcdir"/transparent-xcursor
  for f in "$srcdir"/cursors/usr/share/icons/Adwaita/cursors/*; do
    xcursorgen transparent.cfg "$f"
  done
  cd "$srcdir"
  mv cursors/* "$pkgdir"

  # deduplicate cursors
  hardlink -c "$pkgdir/usr"
}

# vim:set sw=2 sts=-1 et:
