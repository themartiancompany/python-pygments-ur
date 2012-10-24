# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=('python-pygments' 'python2-pygments')
pkgver=1.5
pkgrel=3
pkgdesc='Python syntax highlighter'
arch=('any')
url="http://pygments.org/"
license=('BSD')
makedepends=('python-distribute' 'python2-distribute')
options=('!emptydirs')
source=(http://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz)
sha256sums=('fe183e3886f597e41f8c88d0e53c796cefddc879bfdf45f2915a383060436740')

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
  depends=('python-distribute')
  install=python-pygments.install

  cd "$srcdir/python3-build"

  python3 setup.py install --root="$pkgdir" -O1

  # pygmentize has been moved to the python2-pygments package
  rm "$pkgdir/usr/bin/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-pygments() {
  depends=('python2-distribute')

  cd "$srcdir/python2-build"

  python2 setup.py install --root="$pkgdir" -O1

  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/usr/share/bash-completion/completions/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
