# Maintainer: Bruno Pagani (a.k.a. ArchangeGabriel) <bruno.n.pagani@gmail.com>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Antonio Rojas

pkgbase=powerdevil
pkgname=powerdevil-light
pkgver=5.8.0
pkgrel=1
pkgdesc='Manages the power consumption settings of a Plasma Shell'
arch=('i686' 'x86_64')
url='https://www.kde.org/workspaces/plasmadesktop/'
license=('LGPL')
depends=('plasma-workspace' 'libkscreen')
makedepends=('extra-cmake-modules' 'kdoctools' 'python' 'kdesignerplugin')
conflicts=('powerdevil')
provides=('powerdevil')
source=("http://download.kde.org/stable/plasma/${pkgver}/${pkgbase}-${pkgver}.tar.xz"{,.sig})
sha256sums=('8187e7782a10dd8fba766ab05aa24154ce332fa76273dd09dcb003657a60810e'
            'SKIP')
validpgpkeys=('2D1D5B0588357787DE9EE225EC94D18F7F05997E'  # Jonathan Riddell
              '348C8651206633FD983A8FC4DEACEA00075E1D76'  # KDE Neon
              'D07BD8662C56CB291B316EB2F5675605C74E02CF') # David Edmundson

prepare() {
    mkdir -p build
}

build() {
    cd build
    cmake ../${pkgbase}-${pkgver} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DKDE_INSTALL_LIBDIR=lib \
        -DBUILD_TESTING=OFF
    make
}

package_powerdevil-light() {
    cd build
    make DESTDIR="${pkgdir}" install
}
