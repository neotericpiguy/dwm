pkgname=dwm-git
_pkgname=dwm
pkgver=20161205.e63bf22
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

  cp "$startdir/config.h" .

  git reset --hard HEAD~1
  
#  git apply $startdir/patches/*.diff || true

 git apply $startdir/patches/dwm-5.8.2-fibonacci.diff|| true
 git apply $startdir/patches/dwm-6.1.new-zoomswap.diff|| true
 git apply $startdir/patches/dwm-6.1-push.diff|| true
 git apply $startdir/patches/pertagpatch6.1.diff|| true
 git apply $startdir/patches/tcl.diff|| true
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
