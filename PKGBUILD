# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=('python-pygments' 'python2-pygments' 'pygmentize')
pkgver=2.2.0
pkgrel=2
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
makedepends=('python-setuptools' 'python2-setuptools')
options=('!emptydirs')
source=(https://pypi.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz)
sha256sums=('dbae1046def0efb574852fab9e90209b23f556367b5a320c0bcb871c77c3e8cc')

package_python-pygments() {
  depends=('python-setuptools')

  cd "$srcdir/Pygments-$pkgver"

  python3 setup.py install --root="$pkgdir" -O1

  # pygmentize is shipped in its own package
  rm "$pkgdir/usr/bin/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-pygments() {
  depends=('python2-setuptools')
  install=python2-pygments.install

  cd "$srcdir/Pygments-$pkgver"

  python2 setup.py install --root="$pkgdir" -O1

  # pygmentize is shipped in its own package
  rm "$pkgdir/usr/bin/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_pygmentize() {
  depends=('python-pygments')

  cd "$srcdir/Pygments-$pkgver"

  python3 setup.py install --root="$pkgdir" -O1

  # Remove all files except for usr/bin/pygmentize
  find "$pkgdir" -type f -not -name pygmentize -delete

  # Drop version dependency from console script
  sed -i "s/Pygments==$pkgver/Pygments/g" "$pkgdir/usr/bin/pygmentize"

  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/usr/share/bash-completion/completions/pygmentize"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
