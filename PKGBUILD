# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=('python-pygments' 'python2-pygments')
pkgver=2.0
pkgrel=1
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
makedepends=('python-setuptools' 'python2-setuptools')
options=('!emptydirs')
source=(https://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz)
sha256sums=('4de23e88eeb7570e0425270d1013deff6343d78776dd38aeaf26c98ec3552421')

package_python-pygments() {
  depends=('python-setuptools')
  install=python-pygments.install

  cd "$srcdir/Pygments-$pkgver"

  python3 setup.py install --root="$pkgdir" -O1

  # pygmentize has been moved to the python2-pygments package
  rm "$pkgdir/usr/bin/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-pygments() {
  depends=('python2-setuptools')

  cd "$srcdir/Pygments-$pkgver"

  python2 setup.py install --root="$pkgdir" -O1

  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/usr/share/bash-completion/completions/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
