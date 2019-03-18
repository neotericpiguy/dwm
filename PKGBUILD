pkgname=dwm-git
_pkgname=dwm
pkgver=20190202.cb3f58a
pkgrel=1
pkgdesc="A dynamic window manager for X with useful patches"
arch=('i686' 'x86_64')
url="http://dwm.suckless.org"
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
makedepends=('git')
provides=("$_pkgname")
conflicts=("$_pkgname")
epoch=1

# source=("$_pkgname::git+http://git.suckless.org/dwm"
#         'config.h')
# md5sums=('SKIP'
#          'SKIP')

source=("$_pkgname::git+http://git.suckless.org/dwm")
md5sums=('SKIP')


pkgver(){
  cd $_pkgname
  git log -1 --format='%cd.%h' --date=short | tr -d -
}
        
prepare() {
  cd "$_pkgname"

  cd $srcdir/$_pkgname/

  sed \
  -e 's/CPPFLAGS *=/CPPFLAGS +=/g' \
  -e 's/CFLAGS *=/CFLAGS +=/g' \
  -e 's/LDFLAGS *=/LDFLAGS +=/g' \
  -i config.mk

  git reset --hard 
  rm -f fibonacci.c
  rm -f push.c
  rm -f zoomswap.c

  cp "$startdir/config.h" .

  #fibonacci layout
  git apply $startdir/patches/dwm-5.8.2-fibonacci.diff 
  #Move around client windows
  git apply $startdir/patches/dwm-6.1-push.diff
  #Swap with master
  git apply $startdir/patches/dwm-6.1.new-zoomswap.diff 
  #center column layout
  git apply $startdir/patches/tcl.diff

  #layouts are saved per tag
  git apply $startdir/patches/dwm-pertag-20170513-ceac8c9.diff
  #when ever you move to a window move the cursor
  git apply $startdir/patches/dwm-warp-git-2019.diff

   git apply $startdir/patches/dwm-uselessgap-2019.diff
#  git apply $startdir/patches/dwm-noborder-20160718-56a31dc.diff || true

}

build() {
  cd $_pkgname
  make 
}

package() {
  make -C $_pkgname PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D $_pkgname/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D $_pkgname/README $pkgdir/usr/share/doc/$pkgname/README
}

# vim:set ts=2 sw=2 et:
