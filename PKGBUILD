# Maintainer: MrOz59 <https://github.com/MrOz59>
# Relayout of upstream MrOz59/Hermes-KMS PKGBUILD for branch-per-package repo.

pkgname=(hermes-kms-dkms-git hermes-kms-seatd-git)
pkgbase=hermes-kms-git
_pkgbase=hermes-kms
pkgver=0.4.0
pkgrel=1
pkgdesc="Hermes-KMS zero-copy virtual display DRM/KMS driver (DKMS)"
arch=('any')
url="https://github.com/MrOz59/Hermes-KMS"
license=('GPL2' 'MIT')
makedepends=('git')
source=("git+https://github.com/MrOz59/Hermes-KMS.git")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/Hermes-KMS"
  local _ver
  _ver=$(awk '
    /^#define HERMES_KMS_DRIVER_MAJOR/ { maj=$3 }
    /^#define HERMES_KMS_DRIVER_MINOR/ { min=$3 }
    /^#define HERMES_KMS_DRIVER_PATCH/ { pat=$3 }
    END { print maj"."min"."pat }' kernel/hermes-kms/hermes_kms.c)
  printf '%s.r%s.g%s' "$_ver" \
    "$(git rev-list --count HEAD)" \
    "$(git rev-parse --short HEAD)"
}

package_hermes-kms-dkms-git() {
  cd "$srcdir/Hermes-KMS"

  pkgdesc="Reusable virtual display DRM/KMS driver and public UAPI (DKMS)"
  depends=('dkms' 'acl')
  provides=('hermes-kms')
  conflicts=('hermes-kms')
  install="${_pkgbase}-core.install"

  local _dest="$pkgdir/usr/src/${_pkgbase}-${pkgver}"
  install -dm755 "$_dest"
  cp -a Makefile dkms.conf include kernel "$_dest/"

  sed -i "s/^PACKAGE_VERSION=.*/PACKAGE_VERSION=\"${pkgver}\"/" "$_dest/dkms.conf"

  make DESTDIR="$pkgdir" \
    HERMES_LICENSE_DIR="/usr/share/licenses/$pkgname" \
    install-core-configs install-uapi
}

package_hermes-kms-seatd-git() {
  cd "$srcdir/Hermes-KMS"

  pkgdesc="Optional private seat broker for Hermes-KMS virtual displays"
  depends=('hermes-kms-dkms-git' 'seatd')
  optdepends=('polkit: authorize hermes-kms-setup through pkexec')
  install="${_pkgbase}.install"

  make DESTDIR="$pkgdir" install-broker-configs
}
