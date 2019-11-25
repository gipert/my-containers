# Maintainer: Rémy Oudompheng <remy@archlinux.org>
# Contributor: Firmicus <francois.archlinux.org>
# Contributor: bender02 at gmx dot com

pkgname=asymptote
pkgver=2.61
pkgrel=1
pkgdesc="A vector graphics language (like metapost)"
arch=('x86_64')
url="http://asymptote.sourceforge.net/"
license=("GPL3")
depends=('texlive-core' 'gc' 'freeglut' 'glew' 'gsl' 'fftw' 'libsigsegv')
makedepends=('ghostscript' 'imagemagick'
             'mesa'               # For OpenGL headers
             'texlive-plainextra' # For texinfo
             'python-pyqt5'       # For xasy GUI generation
             'glm')
optdepends=('python-pyqt5: for the xasy GUI'
            'python-cson:  for the xasy GUI')
source="https://sourceforge.net/projects/${pkgname}/files/${pkgver}/${pkgname}-${pkgver}.src.tgz"
sha1sums=('3f9efe2eb59324d89109f6a8cf3148d3d6beef6b')
srcdir="/opt/src"

prepare() {
  cd "${srcdir}"
  wget "${source}"
  gunzip "${pkgname}-${pkgver}.src.tgz"
  tar -xvf "${pkgname}-${pkgver}.src.tar"
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./autogen.sh
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  export CXXFLAGS+=" -I${srcdir}/${pkgname}-${pkgver}"
  ./configure --enable-gc=/usr \
              --prefix=/usr \
              --with-latex=/usr/share/texmf/tex/latex \
              --with-context=/usr/share/texmf/tex/context \
              --enable-offscreen
  make -j"$(nproc)" all
}

check() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make check-all
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make -j1 DESTDIR="${pkgdir}" install-all
  # this dir contains png files that are already embedded in the pdf documentation:
  rm -rf ${pkgdir}/usr/share/info/asymptote

  # copy some data files to their correct location
  mkdir -p "$pkgdir"/usr/share/emacs/site-lisp
  cp "$pkgdir"/usr/share/asymptote/*.el "$pkgdir"/usr/share/emacs/site-lisp
  mkdir -p "$pkgdir"/usr/share/vim/vimfiles/syntax
  cp "$pkgdir"/usr/share/asymptote/*.vim "$pkgdir"/usr/share/vim/vimfiles/syntax
  mkdir -p "$pkgdir"/usr/share/org.kde.syntax-highlighting/syntax
  cd "$pkgdir"/usr/share/asymptote/
  sh asy-kate.sh
  mv asymptote.xml "$pkgdir"/usr/share/org.kde.syntax-highlighting/syntax
}
