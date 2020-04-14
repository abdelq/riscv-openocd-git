# Maintainer: Abdelhakim Qbaich <abdelhakim@qbaich.com>
# Contributor: Jiuyang Liu <liujiuyang1994@gmail.com>
# Contributor: Emil Renner Berthing <aur@esmil.dk>

pkgname=riscv-openocd-git
pkgver=r9141.2e9aad891
pkgrel=1
pkgdesc='Fork of OpenOCD that has RISC-V support'
arch=('x86_64')
url='https://github.com/riscv/riscv-openocd'
license=('GPL')
depends=('libftdi' 'libusb' 'hidapi')
makedepends=('git' 'automake>=1.14' 'autoconf>=2.64')
source=("$pkgname::git+https://github.com/riscv/riscv-openocd.git")
sha1sums=('SKIP')

pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$pkgname"
  git submodule update --init --recursive
}

build() {
  cd "$pkgname"

  ./bootstrap
  ./configure \
    --prefix=/usr \
    --disable-werror \
    --program-prefix=riscv-

  make pkgdatadir="/usr/share/${pkgname%-git}"
}

package() {
  cd "$pkgname"
  make pkgdatadir="/usr/share/${pkgname%-git}" DESTDIR="$pkgdir" install
  rm -r "$pkgdir/usr/share/info"
}
