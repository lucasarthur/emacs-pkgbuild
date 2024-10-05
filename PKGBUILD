# my own build of emacs with some different options
# stolen from official arch emacs build @ https://gitlab.archlinux.org/archlinux/packaging/packages/emacs

pkgname=emacs
pkgver=29.4
pkgrel=1
pkgdesc='The extensible, customizable, self-documenting real-time display editor'
arch=('x86_64')
url='https://www.gnu.org/software/emacs/emacs.html'
license=('GPL3')
depends=(
  gmp
  gnutls
  jansson
  lcms2
  libacl.so
  libasound.so
  libdbus-1.so
  libfontconfig.so
  libfreetype.so
  libgdk-3.so
  libgdk_pixbuf-2.0.so
  libgif.so
  libgio-2.0.so
  libglib-2.0.so
  libgobject-2.0.so
  libgpm.so
  libgtk-3.so
  libharfbuzz.so
  libice
  libjpeg.so
  libncursesw.so
  libotf
  libpango-1.0.so
  libpng
  librsvg-2.so
  libsm
  sqlite libsqlite3.so
  libsystemd.so
  libtiff.so
  libtree-sitter.so
  libwebp.so
  libwebpdemux.so
  libxfixes
  libxml2.so
  m17n-lib
  zlib
  libgccjit
  webkit2gtk
  mailutils
)
source=(https://ftp.gnu.org/gnu/emacs/${pkgname}-${pkgver}.tar.xz)

build() {
  cd ${pkgname}-${pkgver}

  ./configure \
    --sysconfdir=/etc \
    --prefix=/usr \
    --libexecdir=/usr/lib \
    --localstatedir=/var \
    --with-modules \
    --with-tree-sitter \
    --with-xwidgets \
    --with-cairo \
    --with-harfbuzz \
    --with-libsystemd \
    --without-compress-install \
    --with-json \
    --with-mailutils \
    --disable-build-details \
    --with-x-toolkit=gtk3 \
    --with-native-compilation=aot \
    --program-transform-name='s/\([ec]tags\)/\1.emacs/'

  make -j$(nproc)
}

package() {
  cd ${pkgbase}-${pkgver}
  make DESTDIR="${pkgdir}" install

  # remove conflict with ctags package
  mv "${pkgdir}"/usr/bin/{ctags,ctags.emacs}
  mv "${pkgdir}"/usr/share/man/man1/{ctags.1.gz,ctags.emacs.1}

  # fix user/root permissions on usr/share files
  find "${pkgdir}"/usr/share/emacs/${pkgver} -exec chown root:root {} \;
}
