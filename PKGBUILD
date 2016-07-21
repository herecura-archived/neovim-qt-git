# Maintainer: Aaron Abbott <aabmass at gmail dot com>
pkgname=neovim-qt-git
pkgver=20160720.c251a9d
pkgrel=1
pkgdesc="A Qt gui for Neovim (Neovim RPC and GUI using Qt5)."
arch=('i686' 'x86_64')
url="https://github.com/equalsraf/neovim-qt"
license=('custom')
depends=('neovim' 'qt5-base' 'msgpack-c')
makedepends=('git' 'cmake' 'mesa')
conflicts=('neovim-qt')
source=("${pkgname}::git+${url}.git")
md5sums=('SKIP')

pkgver() {
  cd "$pkgname"
  git log -1 --date=short --format="%cd.%h" | tr -d '-'
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
