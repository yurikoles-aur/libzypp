# Maintainer: Yurii Kolesnykov <root@yurikoles.com>
# Contributor: Daan De Meyer <daan.j.demeyer@gmail.com>

pkgbase=libzypp
pkgname=(libzypp libzypp-doc)
pkgver=17.35.2
pkgrel=1
pkgdesc="ZYpp Package Management library"
arch=('x86_64')
url='http://doc.opensuse.org/projects/libzypp/HEAD/'
license=('GPL-2.0-or-later')
makedepends=(
  'boost-libs'
  'gpgme'
  'libproxy'
  'libsigc++'
  'libsolv'
  'libsystemd'
  'libxml2'
  'protobuf'
  'yaml-cpp'
  'asciidoc'
  'boost'
  'cmake'
  'dejagnu'
  'doxygen'
  'expat'
  'git'
  'gnupg'
  'graphviz'
)
source=("${pkgname}-${pkgver}.tgz::https://github.com/openSUSE/${pkgname}/archive/${pkgver}.tar.gz")
sha256sums=('1c84904bd83f2881acb2f9dcab71bd811c831a045a1191f16a7ad7c201a9afd1')

build() {
  cmake \
    -B build \
    -S "${pkgname}-${pkgver}" \
    -D CMAKE_BUILD_TYPE=Release \
    -D CMAKE_INSTALL_PREFIX=/usr \
    -D CMAKE_INSTALL_LIBEXECDIR=lib \
    -D LIB=lib \
    -D CMAKE_SKIP_RPATH=1 \
    -D DISABLE_MEDIABACKEND_TESTS=ON \
	-D ENABLE_BUILD_DOCS=ON \
	-D ENABLE_BUILD_TRANS=ON \
	-D ENABLE_BUILD_TESTS=ON \
	-D ENABLE_ZSTD_COMPRESSION=ON \

  cmake --build build
}

#check() {
#  ctest --test-dir build
#}

package_libzypp() {
  depends=(
    'boost-libs'
    'gpgme'
    'libproxy'
    'libsigc++'
    'libsolv'
    'libsystemd'
    'libxml2'
    'protobuf'
    'yaml-cpp'
  )

  DESTDIR="${pkgdir}" cmake --install build

  # cmake fix (see GH#28)
  mkdir -p "${pkgdir}"/usr/lib/cmake/Zypp
  mv "${pkgdir}"/usr/share/cmake/Modules/* "${pkgdir}"/usr/lib/cmake/Zypp/
  rm -rf "${pkgdir}"/usr/share/{cmake,doc}
}

package_libzypp-doc() {
  arch=('any')
  DESTDIR="${pkgdir}" cmake --install build/doc
  mv "${pkgdir}"/usr/share/doc/packages/libzypp/libzypp "${pkgdir}"/usr/share/doc/libzypp
  rm -rf "${pkgdir}"/usr/share/{doc/packages,man}
}
