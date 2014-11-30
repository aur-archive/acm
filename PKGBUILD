# Maintainer: Anton Bazhenov <anton.bazhenov at gmail>

pkgname=acm
pkgver=5.0
pkgrel=28
pkgdesc="A classic multiplayer flight simulator for Unix/X11"
arch=('i686' 'x86_64')
url="http://www.websimulations.com/ [Down?]"
license=('GPL')
depends=('gdbm' 'libxext')
source=("http://ftp.de.debian.org/debian/pool/main/a/acm/acm_5.0.orig.tar.gz"
        "http://ftp.debian.org/debian/pool/main/a/acm/acm_5.0-28.diff.gz"
        "${pkgname}-arch.patch"
        "${pkgname}.png"
        "${pkgname}.desktop")
md5sums=('c0768937733989eb4b10708a782eaf6a'
         'ea39031a834642928240999933d7f086'
         'ab4bf625b8513e5371a4eccb0990dd5b'
         'cb347ae46c6ef8490486183997d19a14'
         '87fca05fcde186b06322d60d20962e06')

build() {
  cd "${srcdir}/${pkgname}-5.0"

  # Apply Debian patches
  patch -Np1 -i ../${pkgname}_5.0-28.diff

  # Apply Arch patches
  patch -Np1 -i ../${pkgname}-arch.patch

  ./configure --prefix=/usr
  make LDFLAGS=-lgdbm_compat
}

package() {
  cd "${srcdir}/${pkgname}-5.0"

  make bindir="${pkgdir}/usr/bin" \
       prefix="${pkgdir}/usr/share" \
       OBVDIR="${pkgdir}/usr/share/${pkgname}/" \
       INSTALL="/usr/bin/install -c -D" \
       install

  # Install a desktop entry
  install -Dm644 ../${pkgname}.png "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
  install -Dm644 ../${pkgname}.desktop "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  # Install documentation
  mkdir -p "${pkgdir}/usr/share/doc/${pkgname}"
  install -m644 ACM* COPYING README acmdoc.rtf "${pkgdir}/usr/share/doc/${pkgname}"
}
