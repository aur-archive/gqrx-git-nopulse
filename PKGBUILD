# Maintainer: Doug Penner <darwinsurvivor@gmail.com>
# This is a modification of gqrx-git
#   Maintainer: Peter Ivanov <ivanovp@gmail.com>
#   Contributor: Dominik Heidler <dheidler@gmail.com>

pkgname=gqrx-git-nopulse
pkgver=20140411
pkgrel=2
pkgdesc="SDR receiver for Funcube Dongle, RTL-SDR, USRP and OsmoSDR devices without PulseAudio."
arch=('i686' 'x86_64')
url="http://www.oz9aec.net/index.php/gnu-radio/gqrx-sdr"
license=('GPL')
depends=('qt4>=4.6' 'boost-libs' 'fftw' 'libusb' 'gsl' 'alsa-lib' 'libuhd' 'gnuradio' 'gr-osmosdr-git' 'python2-cheetah')
makedepends=('make' 'patch' 'boost' 'git')
conflicts=('gqrx')
_gitroot=git://github.com/csete/gqrx.git
_gitname=gqrx
source=(
    "pulse.patch"
    "21-fcd.rules"
    "gqrx.png"
    "gqrx.desktop"
    "$_gitname::$_gitroot"
)

md5sums=(
    'eda54c93a70f4a225148b83eba680ad9'
    '2be3bf7cba02e90cbbb9d5f6cfdaf68b'
    'f7032a8883c89bd80e0d0fd36f861c59'
    'ecd35521d07adb76cab8f141e77bc1cb'
    'SKIP'
)

build() {
	cd "$srcdir"
	patch -p0 < ../pulse.patch
	cd "$_gitname"
	qmake-qt4
    make clean
	make
}

package() {
	install -m755 -d $pkgdir/etc/udev/rules.d
	install -m755 -d $pkgdir/usr/{bin,share/applications,share/pixmaps}

	cd $srcdir
	
	install -D -m644 21-fcd.rules $pkgdir/etc/udev/rules.d
	install -D -m644 gqrx.desktop $pkgdir/usr/share/applications
	install -D -m644 gqrx.png $pkgdir/usr/share/pixmaps

	cd "gqrx"

	install -D -m755 gqrx $pkgdir/usr/bin
}

