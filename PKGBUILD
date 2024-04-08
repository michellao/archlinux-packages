# Maintainer: Balló György <ballogyor+arch at gmail dot com>
# Maintainer: Bruno Pagani <archange@archlinux.org>

pkgname=keepassxc
pkgver=2.7.7
pkgrel=2
pkgdesc="Cross-platform community-driven port of Keepass password manager"
arch=(x86_64)
url="https://keepassxc.org/"
license=('GPL-2.0-only OR GPL-3.0-only OR LGPL-2.1-only')
depends=(argon2 botan hicolor-icon-theme qt5-x11extras
         minizip qrencode qt5-svg)
makedepends=(asciidoctor cmake qt5-tools)
optdepends=('xclip: keepassxc-cli clipboard support under X server'
            'wl-clipboard: keepassxc-cli clipboard support under Wayland')
checkdepends=()
provides=(org.freedesktop.secrets)
source=(https://github.com/keepassxreboot/keepassxc/releases/download/$pkgver/keepassxc-$pkgver-src.tar.xz{,.sig})
sha256sums=('58fc45ae98e4b3ffb052103014f5b97a41fefd17102c7f56073934dd3a82ee67'
	'SKIP')
# List of signing keys can be found at https://keepassxc.org/verifying-signatures/
validpgpkeys=(BF5A669F2272CF4324C1FDA8CFB4C2166397D0D2
              71D4673D73C7F83C17DAE6A2D8538E98A26FD9C4
              AF0AEA44ABAC8F1047733EA7AFF235EEFB5A2517
              C1E4CBA3AD78D3AFD894F9E0B7A66F03B59076A8)

build() {
  cmake -S keepassxc-$pkgver -B build \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DWITH_XC_ALL=OFF \
    -DWITH_XC_UPDATECHECK=OFF \
	-DWITH_XC_AUTOTYPE=OFF \
	-DWITH_XC_NETWORKING=ON \
	-DWITH_XC_SSHAGENT=ON \
	-DWITH_XC_FDOSECRETS=ON \
	-DWITH_XC_KEESHARE=OFF \
	-DWITH_XC_BROWSER=OFF \
	-DWITH_XC_YUBIKEY=OFF \
	-DWITH_TESTS=OFF \
	-DWITH_APP_BUNDLE=OFF
  cmake --build build
}

package() {
  cmake --build build --target install -- DESTDIR="$pkgdir"
}
