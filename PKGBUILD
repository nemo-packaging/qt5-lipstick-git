## $Id$
# Contributor: Alexey Andreyev <aa13q@ya.ru>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

pkgname=qt5-lipstick-git
_srcname=qt5-lipstick
_project=aa13q # mer-core fork
_branch=aa13q-alpm-qt5.14
pkgver=0.32.21.r11.g82aeca3f
pkgrel=1
pkgdesc="QML toolkit for homescreen creation"
arch=('x86_64' 'aarch64')
url="https://git.sailfishos.org/$_project/lipstick#branch=$_branch"
license=('BSD')
depends=('qt5-base')
makedepends=('git' 'nemo-keepalive-git' 'libresourceqt-git' 'libsystemd' 'libcontentaction-git' 'mce-headers-git' 'qt-mce-git' 'libngf-qt-git' 'ssu-sysinfo-git')
optdepends=()
provides=("${_srcname}")
conflicts=()
source=("${pkgname}::git+${url}")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  ( set -o pipefail
    git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  ) 2>/dev/null
}

prepare() {
    cd "${srcdir}/${pkgname}"
    # TODO: upstream
    sed -i "s|libsystemd-daemon|libsystemd|g" ./src/compositor/alienmanager/alienmanager.pri
    sed -i "s|libsystemd-daemon|libsystemd|g" ./src/compositor/compositor.pri
    #sed -i "s|libsystemd-daemon|libsystemd|g" ./tools/simple-compositor/simple-compositor.pro
    sed -i "s|libsystemd-daemon|libsystemd|g" ./src/src.pro
}

build() {
  cd "${srcdir}/${pkgname}"
  mkdir -p build
  cd build
  qmake -after "SUBDIRS-=doc" ..
  make
}

package() {
  cd "${srcdir}/${pkgname}"
  cd build
  make INSTALL_ROOT="${pkgdir}" install
}
 
