# Maintainer: Daniel Kirchner <daniel@ekpyron.org>
# Contributor: Harley Laue <losinggeneration@gmail.com>
pkgname=oolua2
pkgver=2.0.0.beta1
pkgrel=2
pkgdesc="A C++ binding for Lua, which is intended to ease the embedding of Lua in C++ allowing easy access to tables, functions to be called and types to be pushed and pulled from the stack; also C++ in Lua by binding functions, types and class hierarchies."
arch=(i686 x86_64)
url="http://code.google.com/p/oolua/"
license=('MIT')
depends=(gcc-libs lua)
makedepends=(premake4)
source=(https://oolua.googlecode.com/files/oolua-$pkgver.tar.gz
        lua_includes.patch)
sha512sums=('ebafdbec41086f7f393defc7a76f147641b34b61285115ba9ebc7c5b9d38c76e19e7f4d748b2a03059621e9e40efdf40862fec67c5e694601d6c6e83506ac0c9'
            '83a1dc4e9e291328d0291713500bfdba0e9dfafa9299131d397ed6c96739006d4ec6f433b16f89d58cc4cc8468980c792429691406b5bf90929f374c5c3f0444')

build() {
  cd "$srcdir/oolua-$pkgver"
  
  patch -Np0 -i $srcdir/lua_includes.patch

  premake4 --class_functions=32 oolua-gen
  premake4 gmake

  # We only really want the library and file generator
  make config=release oolua
}

package() {
  cd "$srcdir/oolua-$pkgver"

  # install by hand creating the directories we need since there is no
  # make install
  mkdir -p $pkgdir/usr/{lib,include/oolua,share/licenses/$pkgname}
  cp bin/Release/liboolua.a $pkgdir/usr/lib
  cp include/*.h $pkgdir/usr/include/oolua
  cp licence.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

# vim:set ts=2 sw=2 et:
