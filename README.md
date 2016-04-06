chromium-browser-xdg-app
========================

Compilation of resources to try to build chromium-browser as an xdg-app application.

Requirements:
------------

  * xdg-app >= 0.5
  * xdg-app-builder >= 0.5
  * org.gnome and org.freedesktop Platform and Sdk runtimes

Instructions:
-------------

1. Install the xdg-app repository for GNOME nightly:
```
  wget -O - http://sdk.gnome.org/apt/debian/conf/alexl.gpg.key|sudo apt-key add -
  xdg-app --user remote-add --gpg-key=nightly.gpg gnome-nightly http://sdk.gnome.org/nightly/repo
```
2. Install the required runtimes
```
  xdg-app --user install gnome-nightly org.gnome.Platform
  xdg-app --user install gnome-nightly org.gnome.Sdk
  xdg-app --user install gnome-nightly org.freedesktop.Platform
  xdg-app --user install gnome-nightly org.freedesktop.Sdk
```
3. Build chromium-browser. From this directory:
```
  xdg-app-builder --repo=/path/to/your/xdg-app/repo /path/to/exported/directory \
    org.chromium.ChromiumBrowser
```

WARNING: This is work in progress and it's not guaranteed to work, any comments are welcome.
