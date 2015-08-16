# Maintainer: Patrick Louis <patrick at unixhub dot net>
# 2013-03-27: This PKGBUILD has been created
pkgname=mcwm-beast
packager=venamresm
pkgver=20130327
pkgrel=1
pkgdesc="MCWM with ton of patches"
arch=('i686' 'x86_64')
url="https://github.com/venam/2bwm"
license=('ISC')
depends=('libxcb' 'xcb-proto' 'xcb-util' 'xcb-util-wm')
makedepends=('git')
provides=('2bwm')
conflicts=('2bwm')
source=(mcwm.desktop)
md5sums=('e5f16a47e2d5243c321c3e863e6065d4')

_gitroot="git://github.com/venam/2bwm"
_gitname="2bwm"
_gitbranch="master"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ ! -d "$_gitname" ] ; then
    git clone "$_gitroot"
  fi

  cd "$_gitname"
  git pull origin "$_gitbranch"

  msg2 "GIT checkout done or server timeout"
  msg "Starting make..."

  [ -d "$srcdir/$_gitname-build" ] && rm -rf "$srcdir/$_gitname-build"
  cp -r "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
  LDFLAGS+=" -Wl,--no-as-needed"
  make
}

package() {
  install -o root -g root -m 755 -d "$pkgdir/usr/bin" -d "$pkgdir/usr/man/man1"

  cd "$srcdir/$_gitname-build"
  make "PREFIX=$pkgdir/usr" install
  install -m 644 -D "$srcdir/2bwm.desktop" "$pkgdir/usr/share/xsessions/2bwm.desktop"
}
