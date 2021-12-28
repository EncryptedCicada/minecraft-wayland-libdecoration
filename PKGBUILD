# Maintainer: Ecmel Berk Canlıer <me@ecmelberk.com>
# Contributor: Sven-Hendrik Haase <svenstaro@gmail.com>
# Contributor: philefou <tuxication AT gmail DOT com>
# Contributor: lindquist <tomas@famolsen.dk>
# Contributor: Christoph Siegenthaler <csi@gmx.ch>
# Contributor: Mihai Militaru <mihai.militaru@ephemeros.org>
# Contributor: SpepS <dreamspepser at yahoo dot it>

pkgname=glfw-wayland-minecraft
pkgdesc="A free, open source, portable framework for graphical application development (wayland, patched for Minecraft)"
pkgver=3.4.0
_pkggit=87d5646f5d2bad0562744501633bf8105f59c193
pkgrel=1
arch=('x86_64')
url="https://github.com/Admicos/minecraft-wayland"
license=('custom:ZLIB')
depends=('wayland' 'libxkbcommon' 'libgl')
conflicts=('glfw' 'glfw-wayland')
provides=("glfw=$pkgver")
makedepends=('mesa' 'cmake' 'doxygen' 'vulkan-headers' 'vulkan-icd-loader'
             'extra-cmake-modules' 'wayland-protocols' 'libxi' 'libxrandr'
             'libxcursor' 'libxkbcommon' 'libxinerama')
source=("https://github.com/glfw/glfw/archive/${_pkggit}.tar.gz"
        "0001-Wayland-Set-O_NONBLOCK-on-repeat-timerfd.patch"
        "0002-Wayland-Continue-poll-if-timerfd-can-t-be-read.patch"
        "0003-Don-t-crash-on-calls-to-focus-or-icon.patch"
        "0004-wayland-fix-broken-opengl-screenshots-on-mutter.patch"
        "0005-Add-warning-about-being-an-unofficial-patch.patch"
        "0006-Don-t-crash-getting-scancode-name.patch"
        "0007-libdecor-proper-decorations-with-title-and-window-bu.patch"
        "0008-Add-libdecoration-marker-to-stderr-warning.patch")
sha512sums=('4fb9c8900165bd6e9d64f30017f81471cc4aecf8ea5cc35dbf586ab2f6d2ffc4c765d9b84799fc64bcf8d08a8f693b3fd1967017c2178edf85fcb353c829e0ca'
            'fd7090ae10ef1f52c3f01d95716cbb55a73da4d211608f84ec38abf99aee240d8b75cf84ba4b11e2b0c462397248a060a14ef1955574bb1609051a2653f43f4a'
            '009c1b6b07cdea4f6ada3d068837d9447e79ce2e9c0336b33a742df4fa6b0978914d3a0e45b745205c910bb30fd373e557c5060cd499aad99b13938630102b15'
            '9c6f6e81de1feafeed93988207999d21754c93ff97c8c3158aee43f38b291f4589feaf83e42081445cf89c9209c86e56a0102fccf0d0a97740874dd88e84a746'
            '3c6d317c0c129effd6da48e183228da952a28286acd09abaec4d934031e39a5531d44306e4308c75b33b515113eb54942ca18885edd49b14254af24085de52da'
            'd8e8b704e19652bb30c7799300a1bd0db1619ad17e8e36a3ee51673933eba6a8c47dbd615f4a9a385021bdfaa1ddedb2f24e8c05b670ef5278c71d217e91146e'
            'b35562f1a65ede074e2b1c9caf934062488d391912a41da1ebbc328d2e3500cea31882a9228b9dfad357e571265825aabcfebb3c74bce077ed6e9752c7f865f5'
            'c9893d17241b2a2aa8a02faa0e39f0b41e2b77d1aaee9c6162938265b8a1c52a104068b9837206c27d4d7f1910cf61bc4a32daaeb56ac2066bd39088b27fdc40'
            '12266bb2f86466b933785f47b7638539b1190b513c956297517367e90b059699cab1bfd08f636db45a60a97abe42684eb83534a90ca1cfb25e608c26ba817c30')

prepare() {
  cd "$srcdir/glfw-$_pkggit"
  rm -rf build-wayland || true
  mkdir build-wayland

  for patch in "$srcdir/00"*.patch; do
    echo "Applying patch $patch"
    patch -p1 < "$patch"
  done
}

build() {
  cd "$srcdir/glfw-$_pkggit/build-wayland"

  cmake .. \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_INSTALL_LIBDIR=lib \
      -DBUILD_SHARED_LIBS=ON \
      -DGLFW_USE_WAYLAND=ON \
      -DGLFW_USE_LIBDECOR=ON
}

package() {
  cd "$srcdir/glfw-$_pkggit"/build-wayland

  make DESTDIR=$pkgdir install

  cd ..
  install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
