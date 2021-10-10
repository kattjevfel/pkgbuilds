# Maintainer: katt <magunasu.b97@gmail.com>

pkgname=leanify-git
pkgver=0.4.3.r183.g9be091e
pkgrel=1
pkgdesc='lightweight lossless file minifier/optimizer'
arch=(x86_64 i686)
url=https://github.com/JayXon/Leanify
license=(MIT)
makedepends=(git)
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(git+https://github.com/JayXon/Leanify)
md5sums=('SKIP')

pkgver() {
	git -C Leanify describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	make -C Leanify
}

package() {
	cd Leanify
	install -Dm755 -t "${pkgdir}/usr/bin" leanify
	install -Dm644 -t "${pkgdir}/usr/share/licenses" LICENSE
}
