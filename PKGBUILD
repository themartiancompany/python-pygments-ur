# Maintainer: Evangelos Foutras <foutrelis@gmail.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=('python-pygments' 'python2-pygments')
pkgver=1.4
pkgrel=4
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
makedepends=('python-distribute' 'python2-distribute')
options=('!emptydirs')
source=(http://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz
        utf8-terminal-output.patch)
md5sums=('d77ac8c93a7fb27545f2522abe9cc462'
         '0d9d047796e11050c75470d248aa084c')

build() {
  cd "$srcdir"

  # Fix FS#24804 (Output to terminal fails with Python 3)
  patch -d Pygments-$pkgver -Np1 -i "$srcdir/utf8-terminal-output.patch"

  rm -rf python{,2}-build
  for builddir in python{,2}-build; do
    cp -r Pygments-$pkgver $builddir
    pushd $builddir
    ${builddir%-build} setup.py build
    popd
  done
}

package_python-pygments() {
  depends=('python-distribute')

  cd "$srcdir/python-build"

  python setup.py install --root="$pkgdir" -O1

  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/etc/bash_completion.d/pygments"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-pygments() {
  depends=('python2-distribute')

  cd "$srcdir/python2-build"

  python2 setup.py install --root="$pkgdir" -O1

  # pygmentize is included in the python-pygments package
  rm "$pkgdir/usr/bin/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/python2-pygments/LICENSE"
}

# vim:set ts=2 sw=2 et:
