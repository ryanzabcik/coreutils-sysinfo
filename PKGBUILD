# $Id: PKGBUILD 201684 2013-12-18 05:22:31Z allan $
# Maintainer: Allan McRae <allan@archlinux.org>
# Contributor: judd <jvinet@zeroflux.org>

pkgname=coreutils
pkgver=8.22
pkgrel=3
pkgdesc="The basic file, shell and text manipulation utilities of the GNU operating system"
arch=('i686' 'x86_64')
license=('GPL3')
url="http://www.gnu.org/software/coreutils"
groups=('base')
depends=('glibc' 'pam' 'acl' 'gmp' 'libcap' 'openssl')
install=${pkgname}.install
source=(ftp://ftp.gnu.org/gnu/$pkgname/$pkgname-$pkgver.tar.xz{,.sig}
        coreutils-8.22-shuf-segfault.patch
        sysinfo.patch)
md5sums=('8fb0ae2267aa6e728958adc38f8163a2'
         'SKIP'
         '94f7e6f373f37beb236caabed8fcdb52'
         'SKIP')

prepare() {
  cd ${srcdir}/${pkgname}-${pkgver}
  patch -p1 -i "$srcdir/sysinfo.patch"
  patch -p1 -i ../coreutils-8.22-shuf-segfault.patch
}

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr --libexecdir=/usr/lib --with-openssl \
              --enable-no-install-program=groups,hostname,kill,uptime
  make
}

check() {
  cd ${srcdir}/${pkgname}-${pkgver}
  make RUN_EXPENSIVE_TESTS=yes check
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}
  make DESTDIR=${pkgdir} install
}
