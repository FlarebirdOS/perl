pkgname=perl
pkgver=5.42.0
pkgrel=1
pkgdesc="A highly capable, feature-rich programming language"
arch=('x86_64')
url="https://www.perl.org/"
license=('GPL' 'PerlArtistic')
depends=('glibc' 'libxcrypt')
options=('makeflags' '!purge' 'emptydirs')
source=(https://www.cpan.org/src/5.0/${pkgname}-${pkgver}.tar.xz)
sha256sums=(73cf6cc1ea2b2b1c110a18c14bbbc73a362073003893ffcedc26d22ebdbdd0c3)

build() {
    cd ${pkgname}-${pkgver}

    export BUILD_ZLIB=False
    export BUILD_BZIP2=0

    sh Configure -des                                          \
        -Dprefix=/usr                                          \
        -Dvendorprefix=/usr                                    \
        -Doptimize="${CFLAGS}"                                 \
        -Dlddlflags="-shared ${LDFLAGS}"                       \
        -Dldflags="${LDFLAGS}"                                 \
        -Dprivlib=/usr/lib64/perl5/${pkgver%.*}/core_perl      \
        -Darchlib=/usr/lib64/perl5/${pkgver%.*}/core_perl      \
        -Dsitelib=/usr/lib64/perl5/${pkgver%.*}/site_perl      \
        -Dsitearch=/usr/lib64/perl5/${pkgver%.*}/site_perl     \
        -Dvendorlib=/usr/lib64/perl5/${pkgver%.*}/vendor_perl  \
        -Dvendorarch=/usr/lib64/perl5/${pkgver%.*}/vendor_perl \
        -Dman1dir=/usr/share/man/man1                          \
        -Dman3dir=/usr/share/man/man3                          \
        -Dpager="/usr/bin/less -isR"                           \
        -Duseshrplib                                           \
        -Dusethreads                                           \
        -Dcc=${CHOST}-gcc

    make

    unset BUILD_ZLIB BUILD_BZIP2
}


package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install
}
