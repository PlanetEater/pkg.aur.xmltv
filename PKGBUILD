# Maintainer: Kåre Hampf <khampf@users.sourceforge.net>
# Submitter: Stefan Husmann <stefan-husmann@t-online.de>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Andrew Simmons <andrew.simmons@gmail.com>

prjname=xmltv
pkgname=xmltv-huro
pkgver=0.5.67
pkgrel=1
pkgdesc="Set of utilities to download tv listings and format them in xml - huro grabber"
arch=('any')
url="http://xmltv.org/wiki/"
license=('GPL')
depends=('perl-libwww' 'perl-datetime' 'perl-date-manip'
  'perl-file-slurp'
  'perl-html-tree' 'perl-lingua-en-numbers-ordinate'
  'perl-lingua-preferred' 'perl-term-progressbar'
  'perl-tk-tablematrix'
  'perl-unicode-string'
  'perl-xml-twig' 'perl-xml-writer'
  'perl-xml-treepp'
  'perl-xml-parser' 'perl-date-manip' )
provides=('xmltv')
conflicts=('xmltv')
source=("http://downloads.sourceforge.net/${prjname}/${prjname}-${pkgver}.tar.bz2"
disable-unicode-string.patch)
md5sums=('7f95c24f91a7ac48cf81c32b21dc0492'
         '2a55fecd366f27373633fdc02f6be237')

prepare() {
  echo "NOTE: Disabling recommended but optional Unicode::String"
  echo "      (due to SIGSEGV in build process)"
  cd "$prjname-$pkgver"
  patch -p0 -i $srcdir/disable-unicode-string.patch
  perl Makefile.PL PREFIX=/usr INSTALLDIRS=vendor --components tv_grab_huro

}

build() {
  cd "$prjname-$pkgver"
  make
}

package() {
  cd "$prjname-$pkgver"
  make DESTDIR="$pkgdir/" PREFIX=/usr install
	 
  # remove perllocal.pod and .packlist
  find ${pkgdir} -name perllocal.pod -delete
  find ${pkgdir} -name .packlist -delete
}
