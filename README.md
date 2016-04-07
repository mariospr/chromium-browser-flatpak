chromium-browser-xdg-app
========================

Compilation of resources to try to build chromium-browser as an xdg-app application.

**WARNING**: This is WORK-IN-PROGRESS and it's not guaranteed to work (it just builds for now), any comments are welcome.

Requirements:
------------

  * xdg-app >= 0.5
  * xdg-app-builder >= 0.5
  * appstream-composer (automatically run by xdg-app-builder)
  * org.gnome and org.freedesktop Platform and Sdk runtimes

Instructions:
-------------

(1) Install the xdg-app repository for GNOME nightly:
```
  wget -O - http://sdk.gnome.org/apt/debian/conf/alexl.gpg.key|sudo apt-key add -
  xdg-app --user remote-add --gpg-key=nightly.gpg gnome-nightly http://sdk.gnome.org/nightly/repo
```
(2) Install the required runtimes
```
  xdg-app --user install gnome-nightly org.gnome.Platform
  xdg-app --user install gnome-nightly org.gnome.Sdk
  xdg-app --user install gnome-nightly org.freedesktop.Platform
  xdg-app --user install gnome-nightly org.freedesktop.Sdk
```
(3) Build chromium-browser) From this directory:
```
  xdg-app-builder --repo=/path/to/your/xdg-app/repo \
    /path/to/xdg-app/appdir \
    org.chromium.ChromiumBrowser
```
(4) Add a remote to your local repo and install it:
```
  xdg-app --user remote-add --no-gpg-verify chromium-repo /path/to/your/xdg-app/repo
  xdg-app --user install chromium-repo org.chromium.ChromiumBrowser
```
(5) Run chromium-browser as an xdg-app:
```
  xdg-app run org.chromium.ChromiumBrowser
  xdg-app build-bundle /path/to/your/xdg-app/repo chromium-browser.bundle org.chromium.ChromiumBrowser
```

Note that if you do further changes in the `appdir` (e.g. to the metadata), you'll need to re-publish it in your local repo and update before running it again:
```
  xdg-app build-export /path/to/your/xdg-app/repo /path/to/xdg-app/appdir
  xdg-app --user update org.chromium.ChromiumBrowser
```

Last, you can bundle chromium to a file with the `build-bundle` subcommand:
```
  xdg-app build-bundle /path/to/your/xdg-app/repo chromium-browser.bundle org.chromium.ChromiumBrowser
```
