# Maintainer: Evangelos Foutras <foutrelis@gmail.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=('python-pygments' 'python2-pygments')
pkgver=1.4
pkgrel=3
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
makedepends=('python' 'python-distribute' 'python2' 'python2-distribute')
source=(http://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz)
md5sums=('d77ac8c93a7fb27545f2522abe9cc462')

build() {
  cd "$srcdir"

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

  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/etc/bash_completion.d/pygments2"

  # /usr/bin/pygmentize conflicts with the python-pygmentize package
  mv "$pkgdir/usr/bin/pygmentize"{,2}
  sed -i 's/pygmentize/\02/g' "$pkgdir/etc/bash_completion.d/pygments2"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/python2-pygments/LICENSE"
}

# vim:set ts=2 sw=2 et:
