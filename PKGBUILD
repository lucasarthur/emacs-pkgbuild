# my own build of emacs with some different options
# stolen from official arch emacs build @ https://gitlab.archlinux.org/archlinux/packaging/packages/emacs

pkgname=emacs
pkgver=29.4
pkgrel=1
pkgdesc='GNU Emacs'
arch=('x86_64')
url='https://www.gnu.org/software/emacs/'
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
  libwebpdemux.so
  libxfixes
  libxml2.so
  m17n-lib
  zlib
  libgccjit
  webkit2gtk
  mailutils
  imagemagick
)
source=(https://ftp.gnu.org/gnu/emacs/${pkgname}-${pkgver}.tar.xz)
sha256sums=('ba897946f94c36600a7e7bb3501d27aa4112d791bfe1445c61ed28550daca235')
options=(!strip)

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
    --with-imagemagick \
    --disable-build-details \
    --with-x-toolkit=gtk3 \
    --with-native-compilation=aot \
    --program-transform-name='s/\([ec]tags\)/\1.emacs/'

  make -j$(nproc)
}

package() {
  cd ${pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
  find "${pkgdir}"/usr/share/emacs/${pkgver} -exec chown root:root {} \;
}
