# Maintainer: Ner0
# Contributors: alexwizard, thotypous, jdhore, xduugu, randypenguin, bdheeman, Det

pkgname=chromium-browser-bin
pkgver=LATEST-35
pkgrel=1
pkgdesc="The open-source project behind Google Chrome (Web/HTTP/FTP Browser)"
arch=('i686' 'x86_64')
url="http://www.chromium.org/"
license=('custom:BSD')
depends=('alsa-lib' 'desktop-file-utils' 'flac' 'gconf' 'gtk2' 'nss' 'libxss' 'ttf-font')
optdepends=('ttf-hannom: Unicode Han and Nom (Chinese and Vietnamese) fonts'
            'otf-ipafont: Unicode Gothic/sans and Mincho/serif (Japanese) fonts [AUR]'
            'ttf-indic-otf: Unicode collection various (Indian) language fonts'
            'xdg-utils: for setting a default browser on desktop environments'
            'chromium-libpdf: Chrome PDF plugin integration [AUR]'
            'chromium-pepper-flash: Pepper Flash intergration [AUR]')
provides=('chromium')
conflicts=('chromium')
backup=('etc/chromium/default')
noextract=('chromium.1.gz')
install=chromium.install

_arch='Linux'
[ "$CARCH" = 'x86_64' ] && _arch='Linux_x64'
_pkgver=$(curl -s "http://commondatastorage.googleapis.com/chromium-browser-continuous/$_arch/LAST_CHANGE")
PKGEXT='.pkg.tar'

source=("http://commondatastorage.googleapis.com/chromium-browser-continuous/$_arch/$_pkgver/chrome-linux.zip"
        'chrome-wrapper.patch'
        'chromium.1.gz'
        'chromium.desktop'
        'chromium'
        'default'
        'LICENSE')
md5sums=('SKIP'
         'ea29f290ef70d5b157aa081bafc5f545'
         '1774b5d79cfc67403fb336147a17e9a6'
         '7cc5d72aa4aaf528fb94e32c42a11493'
         '7295ea12f6e24e3143f5686a166f7aba'
         '001a472621cace5c2e140df95c632af1'
         'b689219f39e74e0c0b19f10a1db1839d')

pkgver() {
  echo "$_pkgver"
}

package() {
  install -d "$pkgdir"/{etc/chromium,usr/{bin,lib,share/{applications,licenses/$pkgname,man/man1,pixmaps}}}
  mv chrome-linux "$pkgdir"/usr/lib/chromium

  msg2 "Patching script 'chrome-wrapper'..."
  cd "$pkgdir"/usr/lib/chromium
  patch -s -i "$srcdir"/chrome-wrapper.patch

  msg2 "Making it nice..."
  # Adjust permissions
  find "$pkgdir"/usr/lib/chromium -type d -exec chmod 755 {} ';'
  find "$pkgdir"/usr/lib/chromium -type f -exec chmod 644 {} ';'
  chmod 755 "$pkgdir"/usr/lib/chromium/chrome{,[_-]*}
  chmod 755 "$pkgdir"/usr/lib/chromium/xdg-settings

  msg2 "Finishing up..."
  # Install default settings, wrapper script, desktop, license, manpages and icon
  cd "$srcdir"
  install -m644 default "$pkgdir"/etc/chromium/
  install -m755 chromium "$pkgdir"/usr/bin/
  install -m644 chromium.desktop "$pkgdir"/usr/share/applications/
  install -m644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/
  install -m644 chromium.1.gz "$pkgdir"/usr/share/man/man1/
  mv "$pkgdir"/usr/lib/chromium/chrome.1 "$pkgdir"/usr/share/man/man1/chromium.1
  mv "$pkgdir"/usr/lib/chromium/product_logo_48.png "$pkgdir"/usr/share/pixmaps/chromium.png

  msg2 "Symlinking 'libudev.so.1'..."
  # Symlink missing udev lib
  ln -fs /usr/lib/libudev.so.1 "$pkgdir"/usr/lib/libudev.so.0
}
