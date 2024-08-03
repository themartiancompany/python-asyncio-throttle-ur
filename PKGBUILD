# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_pep517='false'
_py="python"
_pkg=asyncio-throttle
pkgname="${_py}-${_pkg}"
pkgver=1.0.2
pkgrel=1
pkgdesc='Simple, easy-to-use throttler for asyncio'
_http='https://github.com'
_ns='hallazzang'
url="${_http}/${_ns}/${_pkg}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'i686'
  'pentium4'
  'powerpc'
  'mips'
)
license=(
  'MIT'
)
depends=(
  "${_py}"
)
makedepends=(
  "${_py}-setuptools"
  # "${_py}-wheel"
)
[[ "${_pep517}" == true ]] && \
  makedepends+=(
    "${_py}-build"
    "${_py}-installer"
  )
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-cov"
  "${_py}-pytest-xdist"
)
source=(
  "${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  '643005ec2eece8dca28673f60468955b8ce5084c6cd62672bab05327316c9e9a8cc47a6a43b42501e8b0db32e5b636b6911d3e6a270f2d19f173c155c8a77864'
)
b2sums=(
  '13d69d17d314ed89eae18b8a3d0542c50ac58a7c280c5bf11e81d52f8358aa78d437e7fe406242b121261a1f8780e13e6aff130e8b28540baf3b67118fa0724c'
)

prepare() {
  cd \
    "${_pkg}-${pkgver}"
}

build() {
  cd \
    "${_pkg}-${pkgver}"
  export \
    LANG="en_US.UTF-8"
  if [[ "${_pep517}" == 'true' ]]; then
    "${_py}" \
      -m \
        build \
      --wheel \
      --no-isolation
  elif [[ "${_pep517}" == 'false' ]]; then
    LANG="en_US.UTF-8" \
    "${_py}" \
      setup.py \
        build \
          -O1
  fi
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      venv \
    --system-site-packages \
    test-env
  test-env/bin/python \
    -m \
      installer \
    dist/*.whl
  cd \
    tests
  ../test-env/bin/"${_py}" \
    -m pytest \
    -v
}

package() {
  cd \
    ${_pkg}-${pkgver}
  if [[ "${_pep517}" == 'false' ]]; then
    LANG="en_US.UTF-8" \
    "${_py}" \
      setup.py \
        install \
          --root="${pkgdir}" \
          -O1 \
          --skip-build
  elif [[ "${_pep517}" == 'true' ]]; then
    export \
      LANG="en_US.UTF-8"
    "${_py}" \
      -m \
        installer \
      --destdir="$terdir" \
      dist/*.whl
  fi
}

# vim: ts=2 sw=2 et:
