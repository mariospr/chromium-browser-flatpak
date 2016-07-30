chromium-browser-flatpak
========================

Compilation of resources to try to build chromium-browser as an flatpak application.

**WARNING**: This is WORK-IN-PROGRESS and it's not guaranteed to work (it just builds for now), any comments are welcome.

Requirements:
------------

  * flatpak >= 0.5
  * flatpak-builder >= 0.5
  * appstream-composer (automatically run by flatpak-builder)
  * org.gnome Platform and Sdk runtimes

Instructions:
-------------

(1) Install the flatpak repository for GNOME nightly:
```
  wget http://sdk.gnome.org/nightly/keys/nightly.gpg
  flatpak --user remote-add --gpg-import=nightly.gpg gnome-nightly http://sdk.gnome.org/nightly/repo
```
(2) Install the required runtimes
```
  flatpak --user install gnome-nightly org.gnome.Platform
  flatpak --user install gnome-nightly org.gnome.Sdk
```
(3) Build chromium-browser) From this directory:
```
  flatpak-builder --repo=/path/to/your/flatpak/repo \
    /path/to/flatpak/appdir \
    org.chromium.ChromiumBrowser
```
(4) Add a remote to your local repo and install it:
```
  flatpak --user remote-add --no-gpg-verify chromium-repo /path/to/your/flatpak/repo
  flatpak --user install chromium-repo org.chromium.ChromiumBrowser
```
(5) Run chromium-browser as an flatpak:
```
  flatpak run org.chromium.ChromiumBrowser
```

Note that if you do further changes in the `appdir` (e.g. to the metadata), you'll need to re-publish it in your local repo and update before running it again:
```
  flatpak build-export /path/to/your/flatpak/repo /path/to/flatpak/appdir
  flatpak --user update org.chromium.ChromiumBrowser
```

Last, you can bundle chromium to a file with the `build-bundle` subcommand:
```
  flatpak build-bundle /path/to/your/flatpak/repo chromium-browser.bundle org.chromium.ChromiumBrowser
```
