pkgname=materialgram-git
pkgver=git
pkgrel=1
pkgdesc='Unofficial desktop version of Telegram messaging app with Material Design'
arch=('x86_64' 'aarch64')
url="https://github.com/kukuruzka165/materialgram"
license=('GPL3')
depends=('hunspell' 'ffmpeg' 'hicolor-icon-theme' 'lz4' 'minizip' 'openal' 'rnnoise' 'ttf-opensans' 'glibmm-2.68'
         'qt6-imageformats' 'qt6-svg' 'qt6-wayland' 'xxhash'
         'pipewire' 'libxtst' 'libxrandr' 'jemalloc' 'abseil-cpp' 'libdispatch'
         'openssl' 'protobuf')
makedepends=('cmake' 'git' 'ninja' 'python' 'boost' 'fmt' 'range-v3' 'tl-expected' 'microsoft-gsl' 'meson'
             'extra-cmake-modules' 'wayland-protocols' 'plasma-wayland-protocols' 'libtg_owt'
             'gobject-introspection' 'mm-common' 'libxcomposite')
optdepends=('webkit2gtk: embedded browser features'
            'xdg-desktop-portal: desktop integration')
provides=('materialgram')
conflicts=('materialgram')
source=("tdesktop::git+https://github.com/kukuruzka165/materialgram.git#branch=main#submodule=shallow")
sha256sums=('SKIP')
build() {
    cd "$srcdir/tdesktop"
    git submodule update --init --recursive
    git submodule update --init --remote
    cmake \
        -B build \
        -G Ninja \
        -DCMAKE_INSTALL_PREFIX="/usr" \
        -DCMAKE_BUILD_TYPE=Release \
        -DTDESKTOP_API_ID=611335 \
        -DTDESKTOP_API_HASH=d524b414d21f4d37f08684c1df41ac9c \
        -DDESKTOP_APP_DISABLE_AUTOUPDATE=True \
        -DCMAKE_INTERPROCEDURAL_OPTIMIZATION=ON
    ninja -C build
}

package() {
    cd "$srcdir/tdesktop"
    DESTDIR=$pkgdir ninja -C build install
}

pkgver() {
    cd "$srcdir/tdesktop"
    git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

