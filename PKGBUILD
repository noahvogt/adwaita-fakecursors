# Maintainer: Fabian Bornschein <fabiscafe-at-mailbox-dot-org>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Lukas Fleischer <lfleischer@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

_upstream_pkgbase=adwaita-icon-theme
pkgbase="$_upstream_pkgbase-fake-cursors"
pkgname=(
  adwaita-icon-theme
  adwaita-fake-cursors
)
pkgver=46.0
pkgrel=1
pkgdesc="GNOME standard icons - patched to make mouse cursors invincible"
url="https://gitlab.gnome.org/GNOME/adwaita-icon-theme"
arch=(any)
license=(
  CC-BY-SA-3.0
  LGPL-3.0-only
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
_commit=7d2510820199ff7f233511a00895043f3843dbcd  # tags/46.0^0
source=("git+https://gitlab.gnome.org/GNOME/adwaita-icon-theme.git#commit=$_commit"
        "git+https://git.noahvogt.com/noah/transparent-xcursor.git")
b2sums=('SKIP' 'SKIP')

pkgver() {
  cd $_upstream_pkgbase
    git describe --tags | sed -r 's/\.([a-z])/\1/;s/([a-z])\./\1/;s/[^-]*-g/r&/;s/-/+/g'
}

prepare() {
  cd $_upstream_pkgbase
}

build() {
  arch-meson $_upstream_pkgbase build
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
  pkgdesc="GNOME standard cursors - patched to make mouse cursors invincible"
  depends=()
  provides=(adwaita-cursors)
  conflicts=(adwaita-cursors)

  # generate transparent cursor icons
  cd "$srcdir"/transparent-xcursor
  for f in "$srcdir"/cursors/usr/share/icons/Adwaita/cursors/*; do
    xcursorgen transparent.cfg "$f"
  done

  # replace standard cursors with the generated one's
  cd "$srcdir"
  mv cursors/* "$pkgdir"

  # deduplicate cursors
  hardlink -c "$pkgdir/usr"
}

# vim:set sw=2 sts=-1 et:
