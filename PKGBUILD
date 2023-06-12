# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=xf86-video-hwcomposer
pkgver=1
pkgrel=1
pkgdesc='Xorg DDX driver to renderer through HWComposer API on Android devices via libhybris'
url='https://github.com/gemian/xf86-video-hwcomposer'
arch=(i686 x86_64 armv7h aarch64)
license=()
depends=(xorg-server xorgproto drihybris glamor-hybris android-headers)
makedepends=(xorg-server-devel git)
source=('git+https://github.com/gemian/xf86-video-hwcomposer#commit=163cd71436416f4303a99c292aab85354f1f67f8'
        'no-device-condition.patch')
sha256sums=('SKIP'
            '8c088eaebefcfa05c806681d9a904a6be04eb4e45bfc7bc05002989c95fcff1b')

prepare() {
  cd ${pkgname}

  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    echo "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  NOCONFIGURE=1 ./autogen.sh
}

build() {
  cd ${pkgname}
  export CPLUS_INCLUDE_PATH=/usr/iclude/android:/usr/include/android/hybris
  export C_INCLUDE_PATH=/usr/iclude/android:/usr/include/android/hybris
  ./configure --prefix=/usr
  make
}

package() {
  cd ${pkgname}
  make DESTDIR="${pkgdir}" install
}
