# Maintainer: Mihail Strashun <m.strashun@gmail.com> aka Volfram
pkgname=libphobos2
pkgver=2.057
pkgrel=1
pkgdesc="Runtime library & Standard language library for the D programming language"
arch=('i686' 'x86_64')
url="http://www.digitalmars.com/d/2.0/"
source=(http://ftp.digitalmars.com/dmd.$pkgver.zip)
license=('custom')
depends=('d-compiler>=2')
conflicts=('libtango')
provides=('libphobos2='$pkgver)
md5sums=('531c4b60eb002ea8abbe5c80b2eb677d')

if [ $CARCH = 'x86_64' ]
then
	archstr="64"
fi

if [ $CARCH = 'i686' ]
then 
	archstr="32"
fi

build() {
  # Build and install druntime
  cd $srcdir/dmd2/src/druntime 
  make -f posix.mak MODEL=$archstr
  install -Dm644 ./lib/libdruntime.a $pkgdir/usr/lib/libdruntime.a 

  # Build and install standard library binary
  cd $srcdir/dmd2/src/phobos 
  make -f posix.mak MODEL=$archstr
  install -Dm644 ./generated/linux/release/$archstr/libphobos2.a $pkgdir/usr/lib/libphobos2.a 

   # Install standard library *.d modules
   mkdir -p $pkgdir/usr/include/d
   cd $srcdir/dmd2/src/phobos
   cp -Rf std $pkgdir/usr/include/d
   cp -Rf etc $pkgdir/usr/include/d
   cp -f {crc32,index,unittest}.d $pkgdir/usr/include/d

   # Install druntime *.d modules
   mkdir -p $pkgdir/usr/include/d/druntime
   cd $srcdir/dmd2/src/druntime/
   cp -Rf import $pkgdir/usr/include/d/druntime

   # Copy license
   install -Dm644 $srcdir/dmd2/src/phobos/phoboslicense.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
