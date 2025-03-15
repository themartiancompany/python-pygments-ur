# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Timm Preetz <timm@preetz.us>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=pygments
pkgname="${_py}-${_pkg}"
pkgver=2.19.1
pkgrel=1
pkgdesc="Python syntax highlighter"
arch=(
  'any'
)
url="https://${_pkg}.org"
license=(
  'BSD'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-setuptools"
  "${_py}-sphinx"
  "${_py}-wcag-contrast-ratio"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
  "${_py}-hatchling"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-lxml"
)
provides=(
  'pygmentize'
)
conflicts=(
  'pygmentize'
)
replaces=(
  'pygmentize'
)
_pypa="https://files.pythonhosted.org/packages/source"
_src="${_pypa}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
source=(
  "${_src}"
)
sha256sums=(
  '61c16d2a8576dc0649d9f39e089b5f02bcd27fba10d8fb4dcc28173f7a45151f'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
  make \
    -C \
      "doc" \
    html
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  PYTHONDONTWRITEBYTECODE=1 \
  pytest
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      "dist/"*".whl"
  install \
    -vDm644 \
    "LICENSE" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
  mkdir \
    -p \
    "${pkgdir}/usr/share/doc"
  cp \
    -rT \
    "doc/_build/html" \
    "${pkgdir}/usr/share/doc/${pkgname}"
  install \
    -Dm644 \
    "doc/pygmentize.1" \
    -t \
    "${pkgdir}/usr/share/man/man1"
  install \
    -Dm644 \
    "external/pygments.bashcomp" \
    "${pkgdir}/usr/share/bash-completion/completions/pygmentize"
}

# vim:set ts=2 sw=2 et:
