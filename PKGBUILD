# Maintainer: Abdó Roig-Maranges <abdo.roig@gmail.com>

pkgname=extempore-git
pkgver=0.6.0
pkgrel=1
pkgdesc="A cyber-physical programming environment for live coding"
arch=('i686' 'x86_64')
url="http://extempore.moso.com.au"
license=('BSD')
depends=('mesa' 'pcre' 'alsa-lib')
makedepends=('git' 'cmake' 'gcc' 'perl')
optdepends=('jack')
provides=('extempore')
conflicts=('extempore')
source=("git+https://github.com/digego/extempore.git")
md5sums=('SKIP')

pkgver() {
  git --git-dir="${srcdir}/extempore/.git" describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  mkdir -p "${srcdir}/build"
  cd "${srcdir}/build"

  cmake -DCMAKE_INSTALL_PREFIX=/usr \
        -DJACK=ON \
        -DBUILD_DEPS=ON \
        -DPACKAGE=ON \
        ../extempore

  make extempore aot_extended assets
}

package() {
  cd "${srcdir}/build"

  # TODO: fix CMakeLists.txt so it does not rebuild aot_extended at this point.
  make DESTDIR="${pkgdir}/" install
}


# vim:set ts=2 sw=2 et:
