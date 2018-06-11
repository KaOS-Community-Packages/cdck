pkgname=cdck
pkgver=0.7.0
pkgrel=1
pkgdesc="A simple program to verify CD/DVD quality"
arch=('x86_64')
url="http://swaj.net/unix/index.html#cdck"
license=('GPL2')
depends=('glibc' 'gcc-libs')
makedepends=('gcc')
optdepends=('gnuplot')
source=("http://swaj.net/unix/cdck/${pkgname}-${pkgver}.tar.gz"
        "cdck_man.in.patch")
md5sums=('15029d54b99f2e5cf8aae28077669d3f'
         '13bf1bc8668b99cfb0528bad0cae8a91')

prepare() {
  cd "$pkgname-$pkgver"
  msg "### patch"
  patch man/cdck_man.in <"$srcdir/cdck_man.in.patch"
}

build() {
  cd "$pkgname-$pkgver"
  msg "### configure"
  ./configure --prefix=/usr --mandir=/usr/share/man
  make
}

check() {
  cd "$pkgname-$pkgver"
  msg "### make"
  make -k check
}

package() {
  cd "$pkgname-$pkgver"
  msg "### make install"
  make DESTDIR="${pkgdir}/" install
  _docdir=${pkgdir}/usr/share/doc/${pkgname}
  _licdir=${pkgdir}/usr/share/licenses/${pkgname}
  install -dm755 ${_docdir} ${_licdir}
  install -Dpm644 AUTHORS ChangeLog INSTALL NEWS README THANKS TODO ${_docdir}/
  install -Dpm644 COPYING ${_licdir}/
  rm -rf "${pkgdir}/usr/lib"
}
