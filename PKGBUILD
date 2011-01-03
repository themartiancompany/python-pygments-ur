# Maintainer: Evangelos Foutras <foutrelis@gmail.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=python-pygments
pkgver=1.4
pkgrel=1
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
depends=('python2-distribute')
provides=('pygments')
conflicts=('pygments')
replaces=('pygments')
source=(http://pypi.python.org/packages/source/P/Pygments/Pygments-$pkgver.tar.gz)
md5sums=('d77ac8c93a7fb27545f2522abe9cc462')

build() {
  cd "$srcdir/Pygments-$pkgver"

  python2 setup.py install --root="$pkgdir" -O1

  install -Dm644 external/pygments.bashcomp \
                 "$pkgdir/etc/bash_completion.d/pygments"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
