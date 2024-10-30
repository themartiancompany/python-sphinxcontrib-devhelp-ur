# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

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
_pkg=sphinxcontrib-devhelp
_Pkg=sphinx-doc-devhelp
pkgname="${_py}-${_pkg}"
# _name=${pkgname#python-}
pkgver=2.0.0
pkgrel=2
pkgdesc='Sphinx extension which outputs Devhelp document'
arch=(
  any
)
_http="https://github.com"
_ns="sphinx-doc"
url="${_http}/${_ns}/${_pkg}"
license=(
  BSD-2-Clause
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-sphinx"
)
provides=(
  "${_py}-${_Pkg}=${pkgver}"
)
source=(
  "${_pkg}-${pkgver}::git+${url}.git#tag=$pkgver"
)
b2sums=(
  'eb855351bc390f6d7e481720bd6fb31ff59dc75bcaa131e8bf14edae820857600b9222b6105cea6a7740c8bc05d0ef4c2f815bf30099ddeda474d069c12ae0b4'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  PYTHONPATH="sphinxcontrib/devhelp:${PYTHONPATH}" \
  pytest
}

package() {
  local \
    _site_packages
  _site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Symlink license file
  install \
    -dm755 \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_Pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
