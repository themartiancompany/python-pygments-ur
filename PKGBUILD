# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Timm Preetz <timm@preetz.us>

pkgname=python-pygments
pkgver=2.17.2
pkgrel=1
pkgdesc="Python syntax highlighter"
arch=('any')
url="https://pygments.org/"
license=('BSD')
depends=('python')
makedepends=('python-setuptools' 'python-sphinx' 'python-wcag-contrast-ratio'
             'python-build' 'python-installer' 'python-wheel'
             'python-hatchling')
checkdepends=('python-pytest' 'python-lxml')
provides=('pygmentize')
conflicts=('pygmentize')
replaces=('pygmentize')
source=(https://pypi.org/packages/source/p/pygments/pygments-$pkgver.tar.gz)
sha256sums=('da46cec9fd2de5be3a8a784f434e4c4ab670b4ff54d605c4c2717e9d49c4c367')

build() {
  cd pygments-$pkgver
  python -m build --wheel --no-isolation
  make -C doc html
}

check() {
  cd pygments-$pkgver
  PYTHONDONTWRITEBYTECODE=1 pytest
}

package() {
  cd pygments-$pkgver

  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"

  mkdir -p "$pkgdir/usr/share/doc"
  cp -rT doc/_build/html "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 doc/pygmentize.1 -t "$pkgdir/usr/share/man/man1"
  install -Dm644 external/pygments.bashcomp \
    "$pkgdir/usr/share/bash-completion/completions/pygmentize"
}

# vim:set ts=2 sw=2 et:
