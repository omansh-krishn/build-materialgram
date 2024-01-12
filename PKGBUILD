# Maintainer: Omansh Krishn <omansh11597@gmail.com>

pkgname=ayugram-git
pkgver=4.14.3
pkgrel=1
_commithash=59c2cbaabc2db918c90aea30080b81234d1842ce
pkgdesc='Unofficial version of Telegram Desktop with good customization, Ghost mode and message history.'
arch=('x86_64' 'aarch64')
url="https://github.com/AyuGram/AyuGramDesktop"
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
provides=('ayugram-desktop')
conflicts=('ayugram-desktop')
source=("tdesktop::git+https://github.com/AyuGram/AyuGramDesktop#commit=${_commithash}")
sha256sums=('SKIP')
build() {
    cd "$srcdir/tdesktop"
    git submodule update --init --recursive
    cmake \
        -B build \
        -G Ninja \
        -DCMAKE_INSTALL_PREFIX="/usr" \
        -DCMAKE_BUILD_TYPE=Release \
        -DTDESKTOP_API_ID=611335 \
        -DTDESKTOP_API_HASH=d524b414d21f4d37f08684c1df41ac9c \
        -DDESKTOP_APP_DISABLE_AUTOUPDATE=True \
        -DCMAKE_INTERPROCEDURAL_OPTIMIZATION=ON
    ninja -C build -j$(nproc --all)
}

package() {
    cd "$srcdir/tdesktop"
    DESTDIR=$pkgdir ninja -C build install
}

