# Maintainer: carstene1ns <arch carsten-teibes de> - http://git.io/ctPKG

pkgbase=libopenmpt
pkgname=(libopenmpt openmpt123 openmpt123-minimal)
_pkgver=0.2.7299-beta20.2
pkgver=${_pkgver/-/.}
pkgrel=1
pkgdesc='A cross-platform C++ and C library to decode tracked music files (modules) into a raw PCM audio stream.'
arch=('i686' 'x86_64')
url='http://lib.openmpt.org/'
license=('BSD')
depends=('zlib' 'gcc-libs' 'libvorbis' 'mpg123')
makedepends=('sdl2' 'portaudio' 'libsndfile' 'flac' 'help2man' 'libpulse')
source=("http://lib.openmpt.org/files/$pkgname/src/$pkgname-${_pkgver}.tar.gz")
sha256sums=('1ceb6bbd132cf028cb6ed4d1482f0633732b0c3b4ff1880c1a036d5ad5df9cfa')

build() {
  cd $pkgbase-${_pkgver%-*}

  make PREFIX=/usr CONFIG=gcc STATIC_LIB=0 NO_SDL=1 TEST=0 #VERBOSE=2

  # additional, minimal openmpt123 version
  cp bin/openmpt123.norpath bin/openmpt123_full
  rm openmpt123/openmpt123.o bin/openmpt123{,.norpath}
  make PREFIX=/usr CONFIG=gcc STATIC_LIB=0 NO_SDL=1 \
    NO_PORTAUDIO=1 NO_FLAC=1 NO_SNDFILE=1 NO_PULSEAUDIO=1 TEST=0 #VERBOSE=2
  cp bin/openmpt123.norpath bin/openmpt123_minimal
}

package_libopenmpt() {
  cd $pkgbase-${_pkgver%-*}

  make PREFIX=/usr DESTDIR="$pkgdir" OPENMPT123=0 TEST=0 install

  # license
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_openmpt123() {
  pkgdesc='A cross-platform command-line or terminal based module file player.'
  depends=("libopenmpt=$pkgver" 'sdl2' 'portaudio' 'libsndfile' 'flac' 'libpulse')

  cd $pkgbase-${_pkgver%-*}/bin
  install -Dm755 openmpt123_full "$pkgdir"/usr/bin/openmpt123
  install -Dm644 openmpt123.1 "$pkgdir"/usr/share/man/man1/openmpt123.1
  
  # link license
  install -d "$pkgdir"/usr/share/licenses
  ln -s $pkgbase "$pkgdir"/usr/share/licenses/$pkgname
}

package_openmpt123-minimal() {
  pkgdesc='A cross-platform command-line or terminal based module file player (with minimal dependencies).'
  depends=("libopenmpt=$pkgver" 'sdl2')
  conflicts=('openmpt123')

  cd $pkgbase-${_pkgver%-*}/bin
  install -Dm755 openmpt123_minimal "$pkgdir"/usr/bin/openmpt123
  install -Dm644 openmpt123.1 "$pkgdir"/usr/share/man/man1/openmpt123.1

  # link license
  install -d "$pkgdir"/usr/share/licenses
  ln -s $pkgbase "$pkgdir"/usr/share/licenses/$pkgname
}
