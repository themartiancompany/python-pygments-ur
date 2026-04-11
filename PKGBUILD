# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
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

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Evangelos Foutras
#     <evangelos@foutrelis.com>
# Contributors:
#   Timm Preetz
#     <timm@preetz.us>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_source_origin" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _source_origin="pypa"
  fi
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
  _git_http_host="gitlab"
fi
if [[ ! -v "_git_http_host" ]]; then
  _git_http_host="${_git_service}"
fi
if [[ ! -v "_ns" ]]; then
  _ns="themartiancompany"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _archive_format="zip"
      elif [[ "${_tag_name}" == "pkgver" ]]; then
        _archive_format="tar.gz"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    else
      _archive_format="tar.gz"
    fi
  fi
fi
_py="python"
_pyver="$(
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_docs="false"
_pkg=pygments
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=2.19.1
pkgrel=31
_pkgdesc=(
  "Python syntax highlighter"
)
pkgdesc="${_pkgdesc[*]}"
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
  "${_py}-wcag-contrast-ratio"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
  "${_py}-hatchling"
  "${_py}"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "${_py}-sphinx"
  )
fi
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
if [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_source_origin}" == "pypa" ]]; then
    _src="${_pypa}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
  fi
fi
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
  if [[ "${_docs}" == "true" ]]; then
    make \
      -C \
        "doc" \
      html
  fi
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
  if [[ "${_docs}" == "true" ]]; then
    cp \
      -rT \
      "doc/_build/html" \
      "${pkgdir}/usr/share/doc/${pkgname}"
    install \
      -Dm644 \
      "doc/pygmentize.1" \
      -t \
      "${pkgdir}/usr/share/man/man1"
  fi
  install \
    -Dm644 \
    "external/pygments.bashcomp" \
    "${pkgdir}/usr/share/bash-completion/completions/pygmentize"
}

# vim:set ts=2 sw=2 et:
