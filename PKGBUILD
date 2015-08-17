# Maintainer: Gen2ly <toddrpartridge@gmail.com>

pkgname=shadowgrounds-survivor-demo
pkgver=1
pkgrel=1
pkgdesc="Sequel to Shadowgrounds - Science fiction shoot 'em up"
arch=('i686' 'x86_64')
url='http://www.linuxgamepublishing.com/info.php?id=40&'
license=('custom')
install=''
[ "${CARCH}" = "x86_64" ] && depends=('lib32-libgl' 'lib32-gtk' 'lib32-gtk2' 'lib32-libmikmod' 'lib32-libvorbis' 'lib32-mesa' 'lib32-sdl' 'lib32-libxdamage')
[ "${CARCH}" = "i686"   ] && depends=('libgl' 'gtk' 'gtk2' 'libmikmod' 'libvorbis' 'mesa' 'sdl' 'libxdamage')
makedepends=('')
optdepends=('lib32-nvidia-utils: Accelerated 3D with Nvidia driver'
            'lib32-catalyst-utils: Accelerated 3D with ATI driver')
_instname=survivor-demo
source=($pkgname.desktop $_instname.xml)
md5sums=('2ba283da44237892f6d9d589af30daaf'
         '7240a52e9cfa34c67b435cd37a7fde29')


build() {
  cd "$srcdir"
  if [ ! -f $_instname.run ] && [ ! -f $pkgname.tar.gz ]; then
    echo "Downloading demo"
    wget http://demofiles.linuxgamepublishing.com/survivor/survivor-demo.run
  fi
  if [ ! -f $_instname.tar.gz ]; then
    mv $_instname.run $pkgname.tar.gz
    echo "Removing makeself content from installer"
    sed -i '1,376d' $pkgname.tar.gz
  fi
  if [ ! -d $pkgname-$pkgver ]; then
    mkdir $pkgname-$pkgver
  fi
  echo "Extracting archives"
  tar xf $pkgname.tar.gz -C $pkgname-$pkgver
  tar xf $pkgname-$pkgver/.data/data/data.tar.gz -C $pkgname-$pkgver/.data/data/

  # create pkgdir folders
  mkdir -p $pkgdir/usr/bin
  mkdir -p $pkgdir/usr/share/applications
  mkdir -p $pkgdir/usr/share/games/$pkgname
  mkdir -p $pkgdir/usr/share/games/$pkgname/.manifest/scripts
  mkdir -p $pkgdir/usr/share/licenses/$pkgname
  mkdir -p $pkgdir/usr/share/pixmaps

  cd $pkgname-$pkgver

  # licenses
  install -m644 EULA $pkgdir/usr/share/licenses/$pkgname/
  install -m644 README.licenses $pkgdir/usr/share/licenses/$pkgname/

  # game folder
  install -m644 README $pkgdir/usr/share/games/$pkgname/
  install -m755 -D .data/bin/Linux/x86/launcher-bin $pkgdir/usr/share/games/$pkgname/
  install -m755 -D .data/data/survivor-bin $pkgdir/usr/share/games/$pkgname/
  cp .data/data/data*.fbz $pkgdir/usr/share/games/$pkgname/
  cp -r .data/data/data  $pkgdir/usr/share/games/$pkgname/
  cp -r .data/data/lib  $pkgdir/usr/share/games/$pkgname/
  install -m644 $startdir/$pkgname.xml $pkgdir/usr/share/games/$pkgname/.manifest/

  # executable link
  ln -s /usr/share/games/$pkgname/launcher-bin $pkgdir/usr/bin/$pkgname

  # icon/.desktop
  install -m644 .data/icon.xpm $pkgdir/usr/share/pixmaps/$pkgname.xpm
  install -m644 $startdir/$pkgname.desktop $pkgdir/usr/share/applications
}
