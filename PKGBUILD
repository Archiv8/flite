#!/bin/bash

# Created from the original PKGBUILD by Steven Honeyman <stevenhoneyman at gmail com>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154# Maintainer: Antonio Rojas <arojas@archlinux.org>

# [Note]: Built with all libraries enabled


_relname=flite
_prefix=all

pkgname="${_relname}-${_prefix}"
pkgver=2.2
pkgrel=1
pkgdesc="A lightweight speech synthesis engine"
arch=(x86_64)
url="http://www.festvox.org/flite/"
license=(custom)
depends=(
  "alsa-lib"
  )
makedepends=(
  "chrpath")
provides=(
  "flite" "libflite"
  )
conflicts=(
  "flite"
  )
source=(
  "https://github.com/festvox/flite/archive/v$pkgver/${_relname}-$pkgver.tar.gz"
  )
sha512sums=(
  '1ca2f4145651490ef8405fdb830a3b42e885020a7603d965f6a5581b01bed41047d396b38c2ceab138fc0b28d28078db17acd2b5a84c6444cb99d65c581afa72')

# prepare() {
#   cd $pkgname-$pkgver
#   sed '/^#VOXES.*$/d; s/+//g; s/cmu_indic_lex/&\nVOXES = cmu_us_kal16 cmu_us_slt/' config/android.lv >config/archlinux.lv
#   sed -i '/$(INSTALL) -m 755 $(BINDIR)\/flite_time $(DESTDIR)$(INSTALLBINDIR)/d' main/Makefile
# }

build() {
  cd ${_relname}-${pkgver}
  ./configure --prefix=/usr \
    --enable-shared \
    --with-pic \
    --with-audio=alsa \
    --with-lang \
    --with-vox \
    --with-lex

  make
}

package() {
  cd ${_relname}-${pkgver}
  make DESTDIR="$pkgdir" install
  install -D -m644 COPYING "$pkgdir"/usr/share/licenses/${_relname}/LICENSE

  # Fix rpath
  chrpath -d "$pkgdir"/usr/bin/*
}
