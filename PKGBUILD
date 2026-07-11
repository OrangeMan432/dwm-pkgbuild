pkgname=dwm
pkgver=6.8
pkgrel=3
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64' 'aarch64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	dwm.desktop
	start-dwm
	wallpaper.png
	config.h
	colors.h
  gaplessgrid.c
  centeredmaster.c)
_patches=(01-pertag.diff
          02-awesomebar.diff
	  03-dualstatus.diff
	  04-preserveonrestart.diff
	  05-fixborders.diff
	  06-uselessgaps.diff)
source=(${source[@]} ${_patches[@]})

build() {
  cd $srcdir/$pkgname-$pkgver


  for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

  cp $srcdir/config.h config.h
  cp $srcdir/colors.h colors.h
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
  install -m655 -D $srcdir/start-dwm $pkgdir/usr/bin/start-dwm
  install -m655 -D $srcdir/wallpaper.png $pkgdir/usr/share/dwm/wallpaper.png
}
md5sums=('fb14b10a28a4524627fbfa72c567b239'
         '9977d496b38fec05311ac216b0a0f821'
         '980890d24693a073a4dabb997c3ca76f'
         '8525993c4300962ff65cdcac4500bbcd'
         'f6acc09a563119dcdff6c852a56358b5'
         '7827eb20e11351f5708726a3c76b8855'
         '907b5e290ac4bc41bd250837bf5343a9'
         '2488057fd7a5875f4a7f2689dc02d4ab'
         'fe418b7cf2e01f59c05595a8336e6020'
         '46a7ab6a2914d16a0e3cdaee3f605357'
         'a702c720602208bcb22637daf20fe729'
         'fcd79a3e7270817e152dcd305481c558'
         'abb765b73c0bcc162129d4d0b92083b2'
         '10b73a8adbd9a3b486984c1136990bc7')
