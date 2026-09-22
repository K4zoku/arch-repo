# Maintainer: SudoMaker
# Adapted from MrOz59/Hermes for standalone Arch package builds.

pkgname=hermes-streaming
pkgver=0.5.1
pkgrel=1
pkgdesc="Self-hosted game streaming server with virtual display support"
arch=('x86_64')
url='https://github.com/MrOz59/Hermes'
license=('GPL-3.0-only')
install=hermes.install

depends=(
  'avahi'
  'curl'
  'libcap'
  'libdrm'
  'libevdev'
  'libpulse'
  'libva'
  'libx11'
  'libxcb'
  'libxfixes'
  'libxrandr'
  'libxtst'
  'miniupnpc'
  'numactl'
  'openssl'
  'opus'
  'qt6-base'
  'qt6-svg'
  'udev'
)

makedepends=(
  'base-devel'
  'cmake'
  'cuda'
  'git'
  'git-lfs'
  'nodejs'
  'npm'
)

optdepends=(
  'evdi: fallback virtual display support'
  'gamescope: application-only experimental independent client sessions'
  'hermes-kms: zero-copy Hermes virtual displays and independent DRM devices'
  'kscreen: KDE Plasma Wayland virtual-display activation'
  'libva-mesa-driver: AMD GPU encoding support'
  'seatd: private seat brokers for experimental independent client sessions'
  'weston: experimental independent desktop client sessions'
  'wl-clipboard: Hermes text clipboard synchronization on Wayland'
  'xclip: Hermes text clipboard synchronization on X11'
)

conflicts=('hermes')
replaces=('hermes<0.5.0')

source=('Hermes::git+https://github.com/MrOz59/Hermes.git')
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/Hermes"
  local ver
  ver=$(<VERSION)
  printf '%s.r%s.g%s' "$ver" \
    "$(git rev-list --count HEAD)" \
    "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$srcdir/Hermes"
  if [[ ! -d third-party/moonlight-common-c/enet ]]; then
    git submodule update --init --recursive
  fi
  command -v git-lfs >/dev/null 2>&1 && git lfs pull
}

build() {
  cd "$srcdir/Hermes"
  export BRANCH="${BRANCH:-main}"
  export BUILD_VERSION="${BUILD_VERSION:-${pkgver}}"
  export COMMIT="${COMMIT:-$(git rev-parse HEAD)}"

  cmake -S . -B build \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_TESTS=OFF \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DSUNSHINE_EXECUTABLE_PATH=/usr/bin/hermes \
    -DSUNSHINE_ASSETS_DIR=share/hermes
  cmake --build build
}

package() {
  cd "$srcdir/Hermes"
  DESTDIR="$pkgdir" cmake --install build

  rm "$pkgdir/usr/bin/sunshine"
  mv "$pkgdir/usr/bin/sunshine-"* "$pkgdir/usr/bin/hermes"

  if [[ -f "$pkgdir/usr/lib/systemd/user/sunshine.service" ]]; then
    mv "$pkgdir/usr/lib/systemd/user/sunshine.service" \
       "$pkgdir/usr/lib/systemd/user/hermes.service"
  fi
}
