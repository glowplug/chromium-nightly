This is a fork of the AUR chromium-browser-bin package [0].

Changes:
* binary and directory are changed from "chromium" to "chromium-nightly", so it
  does not conflict with the extra/chromium package
* Updated PKGBUILD to be close to the extra/chromium package. Benefits:
    * Fixes the "chromium-nightly -h" option
    * Don't change the default browser each time it is installed

Feel free to send pull requests, as I have very little knowledge about
maintaining packages.

[0] https://aur.archlinux.org/packages/chromium-browser-bin/
