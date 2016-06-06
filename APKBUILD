# Maintainer: Josiah Worcester <josiahw@gmail.com>
pkgname=musl-nscd
pkgver=1.0.1
pkgrel=0
pkgdesc="Implementation of nscd for nsswitch modules for musl"
url="https://github.com/pikhq/musl-nscd"
arch="all"
license="MIT"
depends=""
depends_dev="bison flex"
makedepends="$depends_dev"
install="$pkgname.pre-install $pkgname.post-deinstall"
subpackages="$pkgname-dev $pkgname-doc"
source="
	${pkgname}-${pkgver}.tar.gz::https://github.com/pikhq/musl-nscd/archive/v${pkgver}.tar.gz
	musl-nscd.initd
	musl-nscd.confd
	"

builddir="$srcdir"/$pkgname-$pkgver
build() {
	cd "$builddir"
	./configure \
		--build=$CBUILD \
		--host=$CHOST \
		--prefix=/usr \
		--sysconfdir=/etc \
		--mandir=/usr/share/man \
		--localstatedir=/var \
		|| return 1
	make || return 1
}

package() {
	cd "$builddir"
	make DESTDIR="$pkgdir" install || return 1

	install -m644 -D include/nss.h \
		"$pkgdir"/usr/include || return 1

	install -m644 -D COPYRIGHT \
		"$pkgdir"/usr/share/licenses/$pkgname/COPYRIGHT || return 1

	install -m755 -D "$srcdir"/$pkgname.initd \
		"$pkgdir"/etc/init.d/$pkgname || return 1
	install -m644 -D "$srcdir"/$pkgname.confd \
		"$pkgdir"/etc/conf.d/$pkgname || return 1
}

md5sums="771601b2b7e191fb7bc1941d00397304  musl-nscd-1.0.1.tar.gz
e5870483603c1e0b14b6e987849d2650  musl-nscd.initd
98466a75100ba9fd9d66ef979b1eff03  musl-nscd.confd"
sha256sums="4d2835c48c009b3d9d8fa9579d9cdf15b4d4e60543036066ee76b1854e19a005  musl-nscd-1.0.1.tar.gz
a51abc18bc3014198b01ae86179d1774d87a99f961339d1874accf29619c8a9d  musl-nscd.initd
44e27d4c204ee43dc7a53c856e64408637f87ac1ff09d3efd9b1ebbe8b16686b  musl-nscd.confd"
sha512sums="e5d7393f3ad551ff6af31487fdc0abbb0084f25e386dbd352bcdcbc9844b7ab6caf3fd6b51baa1041eb8353ff63663cfd2be2d3360c8f8bb06df10218795ed0a  musl-nscd-1.0.1.tar.gz
e8150bb601af418b5836f48f157c62b93eadcfdba20880cc61dba154fc24e0fc549b10e4e4642df50aedfa019bc4b955dc06f14148c12aa0e87ae1032b7a1ddb  musl-nscd.initd
d4f7d0dd17e2d805f736c6cd337087c5b65cfdc0f91058e8108b9a4451a14bf5b0a2c6c58f6b9c80f1c36b42ffee67339988ae44adb347d0fc8e86751ec1485c  musl-nscd.confd"
