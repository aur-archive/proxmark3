# Maintainer: fluxius <fluxius AT handgrep DOT se>

pkgname=proxmark3
pkgver=latest
pkgrel=1
pkgdesc="Proxmark3 latest RFID tools and images to listen and emulate everything from Low Frequency (125kHz) to High Frequency (13.56MHz) tags. The package (including clients, tools & images) will be installed in '/opt/proxmark-latest'."
arch=('i686' 'x86_64')
url="http://code.google.com/p/proxmark3/"
license=('WTFPL')
groups=('rfid')
depends=('readline' 'qt4' 'perl' 'wget' 'svn')
makedepends=(pkgextract)
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
source=("LICENSE")
noextract=()

build() {

  _ARCH='i686'
  if [ `uname -m` == 'x86_64' ]; then
    _ARCH='x86_64'
  fi
  if hash arm-none-eabi-gcc 2>/dev/null; then
    echo "We'll be using your 'arm-none-eabi-gcc' to compile proxmark3 images =)"
  else
    wget -P ${srcdir}/ http://sourceforge.net/projects/devkitpro/files/devkitARM/previous/devkitARM_r41-${_ARCH}-linux.tar.bz2/download
    tar jxvf download
    export PATH=${PATH}:${srcdir}/devkitARM/bin/
  fi
  svn checkout http://proxmark3.googlecode.com/svn/trunk/ proxmark3-read-only
  cd ${srcdir}/proxmark3-read-only/
  make
}
package(){
  mkdir -p ${pkgdir}/opt/proxmark-latest
  cp -R ${srcdir}/proxmark3-read-only/tools/ ${pkgdir}/opt/proxmark-latest
  cp ${srcdir}/proxmark3-read-only/client/{proxmark3,flasher,unbind-proxmark} ${pkgdir}/opt/proxmark-latest
  mkdir -p ${pkgdir}/opt/proxmark-latest/images
  cp -R ${srcdir}/proxmark3-read-only/armsrc/obj/{osimage.s19,fpgaimage.s19} ${pkgdir}/opt/proxmark-latest/images
  mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}
  install -D -m644 ${srcdir}/LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE

}

md5sums=('031a8820e88d49c592aebe211a0e1227')
