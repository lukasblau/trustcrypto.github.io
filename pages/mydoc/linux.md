---
title: Using OnlyKey with Linux
tags: [OnlyKey, Linux]
keywords: OnlyKey, Linux, udev
last_updated: Oct, 16, 2020
summary: Guide for using OnlyKey on Linux and creating a UDEV rule for OnlyKey.
sidebar: mydoc_sidebar
permalink: linux.html
folder: mydoc
---


## Using OnlyKey with Linux

### Step 1 - Linux UDEV Rule {#udev-rule}

Linux requires a UDEV rule in order for non-root users to be able to communicate with USB devices. Installing the [OnlyKey App .deb](https://github.com/trustcrypto/OnlyKey-App/releases/download/v5.3.6/OnlyKey_5.3.6_amd64.deb) will also install the UDEV rule automatically or to install manually:

- Go to [https://github.com/trustcrypto/trustcrypto.github.io/blob/master/49-onlykey.rules](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/pages/49-onlykey.rules) and download or create a copy of the file named `49-onlykey.rules` into the Linux directory: `/etc/udev/rules.d/`.

- Use the command `udevadm control --reload-rules && udevadm trigger` or restart system for changes to take effect

To complete this via terminal issue the following commands:

```
$ wget https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/pages/49-onlykey.rules
$ sudo cp 49-onlykey.rules /etc/udev/rules.d/
$ sudo udevadm control --reload-rules && udevadm trigger
```

### Step 2 - Install OnlyKey Desktop App {#install-app}

For Debian user's install the DEB below.

[<i class="fa fa-linux fa-2x"></i> **Linux**](https://github.com/trustcrypto/OnlyKey-App/releases/download/v5.3.6/OnlyKey_5.3.6_amd64.deb)

For other Linux users you may install the OnlyKey app via [snapcraft](https://snapcraft.io/onlykey-app)

```
$ snap install --beta --devmode onlykey-app
```

At time of writing, an issue is open with snapcraft to allow USB permissions, this requires manual approval from snapcraft. Once this is complete the app can be installed without dev-mode. Additional alternatives are mentioned below:

**Install Brave/Chromium Browser**
The app is also available as a Chrome app which is supported in Brave and Chromium browsers:

Follow instructions here to install [Brave browser](https://brave-browser.readthedocs.io/en/latest/installing-brave.html#linux)

Launch Brave browser

```
$ brave-browser
```

Click [here](https://chrome.google.com/webstore/detail/onlykey-configuration/adafilbceehejjehoccladhbkgbjmica) to browse to the OnlyKey Configuration app on the Chrome Web Store and select 'Add to Chrome'

**Extract and run directly**
As an alternative you may also extract the .DEB and run the application directly:

```
$ ar xf OnlyKey*.deb
$ tar xf data.tar.xz
```

Copy the OnlyKey directory to where you want the app i.e.

```
$ sudo cp -r opt/OnlyKey/ /opt/
```

Fedora requires additional dependency

```
$ sudo dnf install libXScrnSaver
```

To launch the app run the nw file located in the OnlyKey directory, you may want to create a symlink to launch the nw file.

### Step 3 - Customization {#custom-app}

You may want to also install the OnlyKey CLI app. Follow instructions [here](https://docs.crp.to/command-line.html)

This permits additional customizations such as scripting to automatically running commands when OnlyKey is inserted.

- One requirement of TOTP (Time-based One-time Password) is having the correct time. If OnlyKey is used on a system where the OnlyKey app is not running it will display “NOTSET” instead of the OTP code. Because OnlyKey has no battery it requires an app to send it the correct time to be able to generate TOTP codes. If you have OnlyKey command-line utility installed, adding the following to UDEV rule will automatically set the current time on OnlyKey every time you plug it: RUN+="/usr/local/bin/onlykey-cli settime"
Additonal details are provided in the udev rule here - [https://github.com/trustcrypto/trustcrypto.github.io/blob/master/49-onlykey.rules](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/pages/49-onlykey.rules)

- Another example is provided for OnlyKey to blink blue whenever the udev rule is run. This is useful for visual verification of LUKS disk decryption, additional details available [here](https://docs.crp.to/full-disk-encryption.html)


{% include links.html %}
