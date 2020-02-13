# Maintainer: Ingo Heimbach <i.heimbach@fz-juelich.de>

pkgname="gr-framework"
pkgver="0.46.0"
pkgrel="2"
pkgdesc="A universal framework for cross-platform visualization applications."
arch=("i686" "x86_64" "armv6h" "armv7h" "aarch64")
url="https://gr-framework.org"
license=("MIT")
depends=("bzip2" "cairo" "fontconfig" "freetype2" "ghostscript" "glfw-x11" \
         "libjpeg-turbo" "libpng" "libtiff" "libx11" "libxft" "libxt" "pixman" \
         "qhull" "qt5-base" "zlib")
makedepends=("cmake")
optdepends=("ffmpeg: video support")
source=("https://github.com/sciapp/gr/archive/v${pkgver}.tar.gz"
        "${pkgname}-${pkgver}.patch")
sha256sums=("c466ae98fd26ac8a30d1b35a899201eaf0ede593b0a3f61f806c49261acb6982"
            "91475fcd6bb066206a39d0991a70c7176912b01d8c166f5a607b83045d530195")

prepare() {
    cd "${srcdir}/gr-${pkgver}" || return
    patch -Np1 -i "${srcdir}/${pkgname}-${pkgver}.patch" && \
    echo "${pkgver}" > version.txt
}

build() {
    cd "${srcdir}/gr-${pkgver}" || return
    cmake -DCMAKE_INSTALL_PREFIX=/usr/gr \
          -DCMAKE_BUILD_TYPE=Release \
          -DGR_USE_BUNDLED_LIBRARIES=OFF \
          -S . \
          -B build && \
    cmake --build build
}

package() {
    cd "${srcdir}/gr-${pkgver}" || return
    DESTDIR="${pkgdir}" cmake --install build
}
