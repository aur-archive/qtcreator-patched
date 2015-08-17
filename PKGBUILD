# $Id$
# Maintainer: Imanol Celaya <ornitorrincos@archlinux-es.org>
# Maintainer: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Lukas Jirkovsky <l.jirkovsky@gmail.com>
# Contributor: Dan Vratil <progdan@progdansoft.com>
# Contributor: thotypous <matiasΘarchlinux-br·org>
# Contributor: delor <bartekpiech gmail com>
# Contributor: m0rph <m0rph.mailbox@gmail.com>

pkgname="qtcreator-patched"
pkgver=2.6.2
_pkgver=2.6.2
pkgrel=7
pkgdesc='QtCreator with custom patches'
arch=('i686' 'x86_64')
url='http://qt.nokia.com/products/developer-tools'
license=('LGPL')
provides=('qtcreator')
depends=('qt')
makedepends=('qt>=4.8.0' 'qt-private-headers' 'git')
options=('docs')
optdepends=('qt-doc: for the integrated Qt documentation'
            'gdb: for the debugger'
            'cmake: for cmake project suppport'
            'openssh-askpass: for ssh support'
            'git: for git support'
            'mercurial: for mercurial support'
            'bzr: for bazaar support'
            'valgrind: for analyze support')
install=qtcreator.install
source=("http://releases.qt-project.org/qtcreator/${_pkgver}/qt-creator-${_pkgver}-src.tar.gz"
        'qtcreator.desktop' 'separate-pod-highlight.patch' 'pointers-and-references-fix.patch'
        'add-right-sidebar.patch' 'disable-constructors-highlight.patch' 'bookmark.png'
        'breakpoint-disabled.png' 'breakpoint-pending.png' 'breakpoint.png' 'error.png'
        'info.png' 'location.png' 'warning.png')
md5sums=('4700deb89e8cf92239015d7d70f0dcdd'
         '5aa242e0262fa22f75c3b59d3a4ec198'
         '3184889399e97a47353a2a0d2941003a'
         '10842ad52dfe102ba857946388b1293c'
         'ca7c060a14af38ca4704a6374447dc9c'
         '3aaf75a20135e7a4abbeb60113752b68'
         '0eadf586a1d2088769588620fa57684c'
         '676f4b5faea438237783f0fd94d70528'
         '888eb792bb2f80553fd6a36554006611'
         '7b0427008d99a38c719796785c36b548'
         '13a319c2c5e163aa87a58d7fb7716cbe'
         '751c5c49aae0f4d3a663272dbc01dc47'
         '3bf5686caa83d20dba321191174d2869'
         'ae309a54a5803cee028586a140f21bdb')

build() {
  cd ${srcdir}/qt-creator-${pkgver}-src/
  patch -p2 -i ${srcdir}/../separate-pod-highlight.patch
  patch -p2 -i ${srcdir}/../pointers-and-references-fix.patch
  patch -p2 -i ${srcdir}/../add-right-sidebar.patch
  patch -p2 -i ${srcdir}/../disable-constructors-highlight.patch
  
  cp ${srcdir}/../bookmark.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/bookmarks/images/bookmark.png
  cp ${srcdir}/../error.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/projectexplorer/images/compile_error.png
  cp ${srcdir}/../warning.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/projectexplorer/images/compile_warning.png
  cp ${srcdir}/../info.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/debugger/images/log.png
  cp ${srcdir}/../error.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/debugger/images/error.png
  cp ${srcdir}/../breakpoint.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/debugger/images/breakpoint_16.png
  cp ${srcdir}/../breakpoint-disabled.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/debugger/images/breakpoint_disabled_16.png
  cp ${srcdir}/../breakpoint-pending.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/debugger/images/breakpoint_pending_16.png
  cp ${srcdir}/../location.png ${srcdir}/qt-creator-${_pkgver}-src/src/plugins/debugger/images/location_16.png

  cd ..

  [[ -d build ]] && rm -r build
  mkdir build && cd build

  qmake ${srcdir}/qt-creator-${_pkgver}-src/qtcreator.pro
  make
}

package() {
  cd ${srcdir}/build

  make INSTALL_ROOT="${pkgdir}/usr/" install

  install -Dm644 ${srcdir}/qtcreator.desktop ${pkgdir}/usr/share/applications/qtcreator.desktop
  install -Dm644 ${srcdir}/qt-creator-${_pkgver}-src/LGPL_EXCEPTION.TXT ${pkgdir}/usr/share/licenses/qtcreator/LGPL_EXCEPTION.TXT
}
