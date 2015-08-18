# -*- mode: sh; -*-
# Contributor: Guillaume Clément <gclement@baobob.org>

pkgname=xf86-video-modesetting-git
pkgver=20121105
pkgrel=1
pkgdesc="Basic modesetting driver for Xorg"
arch=('i686' 'x86_64')
url=('http://cgit.freedesktop.org/xorg/driver/xf86-video-modesetting')
license=('custom')
depends=('libdrm' 'udev')
makedepends=('git' 'xorg-server-devel' 'libx11' 'resourceproto' 'libxss')
provides=('xf86-video-modesetting')
conflicts=('xf86-video-modesetting')

_gitroot='git://anongit.freedesktop.org/xorg/driver/xf86-video-modesetting'
_gitname='xf86-video-modesetting'

build() {
  if [ -d $_gitname ] ; then
      pushd $_gitname
      git pull origin
      popd
      msg 'The local files are updated.'
  else
      git clone $_gitroot
  fi

  msg 'GIT checkout done or server timeout'

  [ -d build ] && rm -rf build
  cp -r $_gitname build
  cd build

  msg 'Starting make...'
  ./autogen.sh --prefix=/usr

}

package() {
  cd build

  make DESTDIR="$pkgdir" install

  install -D -m644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}
