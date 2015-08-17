# Maintainer: Barton Cline <barton bcdesignswell com>
# Contributor: George Nassar <george@providentdata.com>
# Contributor: Jelle van der Waa <jelle vdwaa nl>
# Contributor: Stéphane Gaudreault <stephane@archlinux.org>
# Contributor: Dale Blount <dale@archlinux.org>

pkgname=synergy-beta
pkgver=1.4.9
pkgrel=1
pkgdesc="Share a single mouse and keyboard between multiple computers"
url="http://synergy-foss.org"
arch=('i686' 'x86_64')
depends=('gcc-libs' 'libxtst' 'libxinerama' 'bash')
conflicts=('synergy')
provides=('synergy')
license=('GPL2')
makedepends=('libxt' 'cmake' 'python2')       # used by configure to test for libx11...
backup=('etc/synergy.conf')
source=("http://synergy.googlecode.com/files/synergy-$pkgver-Source.tar.gz" synergys.rc)
md5sums=('fa86608dac784ff14cb38ece204bf43f'
         '8f8c01add9bf6e3ae9f37a36ca6345b6')

build() {
  cd "${srcdir}/synergy-${pkgver}-Source"
  sed -i -e 's/^python /python2 /g' ./hm.sh
  ./hm.sh conf -g1
  ./hm.sh build
  # Don't do this due to the Qt dependency
  # from this directory traverse src/gui
  #cd src/gui
  #qmake && make
  # and POOF! the synergy executible is in ../../bin
}

package() {
  cd "${srcdir}/synergy-${pkgver}-Source"

  # install binary
  install -d "$pkgdir/usr/bin/"
  install -Dm755 bin/synergyc "$pkgdir/usr/bin/"
  install -Dm755 bin/synergys "$pkgdir/usr/bin/"
  # install the gui
  #install -Dm755 bin/synergy "$pkgdir/usr/bin/"
  
  
  # install desktop entries in /usr/share/applications/
  #install -d "${pkgdir}/usr/share/applications"
  # originally from res/synergy.desktop (could still use that one)
  #install -Dm644 ../../synergy.desktop "${pkgdir}/usr/share/applications" # true
  
  # install icons in /usr/share/pixmaps/?synergy?
  #install -d "${pkgdir}/usr/share/pixmaps"
  # originally from res/synergy.ico
  #install -Dm644 ../../synergy.png "${pkgdir}/usr/share/pixmaps" # true

  # install rc.d script  and config
  install -d "${pkgdir}/etc/rc.d"
  install -Dm644 doc/synergy.conf.example-basic "${pkgdir}/etc/synergy.conf" # true
  install -Dm755 "$srcdir/synergys.rc" "${pkgdir}/etc/rc.d/synergys" # true
}

