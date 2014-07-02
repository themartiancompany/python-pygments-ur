# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=('python-pygments' 'python2-pygments')
pkgver=1.6
pkgrel=4
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
makedepends=('python-setuptools' 'python2-setuptools')
options=('!emptydirs')
source=(https://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz
        make-pygments.lexers.guess_lexer_for_filename-py3-compatible.patch)
sha256sums=('799ed4caf77516e54440806d8d9cd82a7607dfdf4e4fb643815171a4b5c921c0'
            '15cf8323ce343d32cbf78d35ab20001ce3204abe90b68a80607c7aea41499f07')

prepare() {
  cd "$srcdir/Pygments-$pkgver"

  patch -Np1 -i "$srcdir/make-pygments.lexers.guess_lexer_for_filename-py3-compatible.patch"
}

build() {
  cd "$srcdir"

  rm -rf python{2,3}-build
  for builddir in python{2,3}-build; do
    cp -r Pygments-$pkgver $builddir
    pushd $builddir
    ${builddir%-build} setup.py build
    popd
  done
}

package_python-pygments() {
  depends=('python-setuptools')
  install=python-pygments.install

  cd "$srcdir/python3-build"

  python3 setup.py install --root="$pkgdir" -O1

  # pygmentize has been moved to the python2-pygments package
  rm "$pkgdir/usr/bin/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-pygments() {
  depends=('python2-setuptools')

  cd "$srcdir/python2-build"

  python2 setup.py install --root="$pkgdir" -O1

  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/usr/share/bash-completion/completions/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
