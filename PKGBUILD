# Maintainer: Daniel Hillenbrand <codeworkx [at] bbqlinux [dot] org>
# Shamelessly stolen from:
# "jre6" & "jdk6" Maintainer: Ethan Hall
# "jre6" & "jdk6" Contributors: Guillaume ALAUX, Daniel J Griffiths, Jason Chu, Geoffroy Carrier, Thomas Dziedzic, Dan Serban

pkgname=jre6-compat
pkgver=6u51
pkgrel=09
epoch=2
pkgdesc="Java 6 Runtime Environment designed to work alongside OpenJDK7"
url=http://www.oracle.com/technetwork/java/javase/downloads/index.html
arch=(i686 x86_64)
license=(custom)
depends=(glibc libxtst)
makedepends=(lynx)
provides=('java-runtime=6' j2re)
conflicts=('java-runtime=6' j2re)
replaces=(j2re)
install=jre.install
#DLAGENTS=('http::/usr/bin/curl -fLC - --retry 3 --retry-delay 3 -o %o %u --header "Cookie:oraclelicensejdk-${pkgver}-oth-JPR=accept-securebackup-cookie;gpw_e24=http://edelivery.oracle.com"')
DLAGENTS=('http::/usr/bin/curl -LC - -b "oraclelicense=a" -O') 
source=("http://download.oracle.com/otn-pub/java/jdk/$pkgver-b$pkgrel/jdk-$pkgver-linux-i586.bin"
        'javaws-launcher'
        'construct.sh')
md5sums=('ab18c2e0244f09dff0d49a328ebe5775'
         '45c15a6b4767288f2f745598455ea2bf'
         '70b34ef3d5b997e7c15b1b50053d3e37')
         
[ "${CARCH}" == 'i686' ] && _arch=i586

[ "${CARCH}" == 'x86_64' ] && _arch=x64 && source[0]="http://download.oracle.com/otn-pub/java/jdk/${pkgver}-b${pkgrel}/jdk-${pkgver}-linux-x64.bin" && md5sums[0]='81e97879481bf32e9af63206b121e6f2'

package()
{

  rm -rf unbundle-jdk
  rm -rf linux-jdk

  cd $srcdir
  
  mkdir unbundle-jdk
  cd unbundle-jdk

  sh ../jdk-$pkgver-linux-$_arch.bin -noregister

  cd ..

  echo ${linux-jdk}
  sh construct.sh unbundle-jdk linux-jdk linux-jre

  mkdir -p "${pkgdir}"/usr/lib/jvm/java-6-oracle/
  mv linux-jdk/jre "${pkgdir}"/usr/lib/jvm/java-6-oracle/

  mkdir -p "${pkgdir}"/usr/share/licenses/jre6-oracle
  install -m644 "${pkgdir}"/usr/lib/jvm/java-6-oracle/jre/COPYRIGHT "${pkgdir}"/usr/share/licenses/jre6-oracle
  install -m644 "${pkgdir}"/usr/lib/jvm/java-6-oracle/jre/LICENSE "${pkgdir}"/usr/share/licenses/jre6-oracle
  install -m644 "${pkgdir}"/usr/lib/jvm/java-6-oracle/jre/THIRDPARTYLICENSEREADME.txt "${pkgdir}"/usr/share/licenses/jre6-oracle

  install "${startdir}"/javaws-launcher "${pkgdir}"/usr/lib/jvm/java-6-oracle/jre/bin/javaws-launcher

}

