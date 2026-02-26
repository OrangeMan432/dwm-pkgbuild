pkgname=dwm
pkgver=6.7
pkgrel=2
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64' 'aarch64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	dwm.desktop
	config.h
  gaplessgrid.c
  centeredmaster.c)
_patches=(01-pertag.diff
          02-awesomebar.diff
	  03-dualstatus.diff)
source=(${source[@]} ${_patches[@]})

build() {
  cd $srcdir/$pkgname-$pkgver


  for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

  cp $srcdir/config.h config.h
  cp $srcdir/gaplessgrid.c gaplessgrid.c
  cp $srcdir/centeredmaster.c centeredmaster.c

  sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
md5sums=('c3bc22a236e5ba6fc713f3a1faa56509'
         '939f403a71b6e85261d09fc3412269ee'
         '58d2bbbc4d6ee6f537867fdb6f5b74dc'
         '907b5e290ac4bc41bd250837bf5343a9'
         '2488057fd7a5875f4a7f2689dc02d4ab'
         'fe418b7cf2e01f59c05595a8336e6020'
         'dc5e132a90a3b9da947c26e68399ac39'
         '91d8bad2a088fac84b34d4960375d86a')
