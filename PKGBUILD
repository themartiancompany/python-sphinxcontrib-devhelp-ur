# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_name=sphinxcontrib_devhelp
pkgname=python-sphinxcontrib-devhelp
pkgver=1.0.4
pkgrel=1
pkgdesc='Sphinx extension which outputs Devhelp document'
arch=('any')
url=https://github.com/sphinx-doc/sphinxcontrib-devhelp
license=('BSD')
makedepends=('python-build' 'python-flit-core' 'python-installer')
checkdepends=('python-pytest' 'python-sphinx')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz")
sha256sums=('4fd751c63dc40895ac8740948f26bf1a3c87e4e441cc008672abd1cb2bc8a3d1')
b2sums=('e8e7460259f48c7373fe97ee70a5c358a5df21233d165645a15ba72f3fb1fd7bc3fba367efd56b27ee5861b6bed6fd14f9e22acd08b345e70b5241b3366e2bff')

build() {
  cd $_name-$pkgver
  python -m build --wheel --skip-dependency-check --no-isolation
}

check() {
  cd $_name-$pkgver
  pytest
}

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/$_name-$pkgver.dist-info/LICENSE \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
