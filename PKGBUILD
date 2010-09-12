# Maintainer: Evangelos Foutras <foutrelis@gmail.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=python-pygments
pkgver=1.3.1
pkgrel=3
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
depends=('setuptools')
provides=('pygments')
conflicts=('pygments')
replaces=('pygments')
source=(http://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz)
md5sums=('54be67c04834f13d7e255e1797d629a5')

build() {
  cd "$srcdir/Pygments-$pkgver"

  python2 setup.py install --root="$pkgdir" -O1

  install -Dm644 external/pygments.bashcomp \
                 "$pkgdir/etc/bash_completion.d/pygments"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
