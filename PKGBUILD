# Maintainer: Aaron Abbott <aabmass at gmail dot com>
pkgname=neovim-qt-git
pkgver=r219.49a61e0
pkgrel=2
pkgdesc="A Qt gui for Neovim (Neovim RPC and GUI using Qt5)."
arch=('i686' 'x86_64')
url="https://github.com/equalsraf/neovim-qt"
license=('custom')
groups=()
# not sure which qt5 dependency to add
depends=('neovim' 'qt5-base' 'msgpack-c' 'libxkbcommon-x11')
makedepends=('git' 'cmake')
provides=()
conflicts=('neovim-qt')
replaces=()
backup=()
options=()
install=
source=("${pkgname}::git+${url}.git")
noextract=()
md5sums=('SKIP')

pkgver() {
  cd "$pkgname"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  mkdir -p "${pkgname}/build"
  cd "${pkgname}/build"

  cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release \
    -DUSE_SYSTEM_MSGPACK=ON -DCMAKE_INSTALL_PREFIX=/usr ..

  make
}

package() {
  cd "${pkgname}/build"

  # cmake isn't configured to install anything, do it on our own
  install -D -m755 bin/nvim-qt "${pkgdir}/usr/bin/nvim-qt"
  install -D -m644 lib/libneovim-qt.a "${pkgdir}/usr/lib/libneovim-qt.a"

  # install the custom license
  install -D -m644 ../LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
