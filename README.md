Brother, I'll update the content. I'm new to Github so using your stuff as a reference.

![debian-xfce.jpg](debian-xfce.jpg)

## Fedora Xfce4 Install Guide

The standard Fedora installation process for Xfce desktop includes additional packages that may not be necessary for many users. This guide will allow you to install a minimal Xfce desktop, adding additional packages as needed.

## Requirements

* A Fedora netinstall LIVE USB.

* sudo privileges to install packages and run optional install script.

## ISO for installing Fedora

* [Download Fedora Everything net installer](https://alt.fedoraproject.org/)

## Installing Debian without a desktop environment

As you progress through the debian installation, towards the end you will be presented with the following screen for Software selection:

![debian-installer.jpg](debian-installer.jpg)

Uncheck **Debian desktop environment** to install a minimal debian system.

## Update sources to testing or unstable (optional)

Update sources to `trixie`. The current testing branch.

`sudo nano /etc/apt/sources`:

```bash
deb http://deb.debian.org/debian/ trixie main
#deb-src http://deb.debian.org/debian/ trixie main

deb http://security.debian.org/debian-security trixie-security main
#deb-src http://security.debian.org/debian-security trixie-security main

deb http://deb.debian.org/debian/ trixie-updates main
#deb-src http://deb.debian.org/debian/ trixie-updates main
```

Add `contrib non-free-firmware` after each `main` entry if you need special drivers or additional firmware.

The other option would be debian sid. Update `sources` as follows:

```bash
deb http://deb.debian.org/debian/ unstable main
#deb-src http://deb.debian.org/debian/ unstable main
```

Upgrade your system:

```bash
sudo apt update && apt upgrade
```

Reboot to load updated kernel and services.

## Quick install Xfce and required packages

```bash
git clone https://github.com/coonrad/Debian-Xfce4-Minimal-Install.git
cd Debian-Xfce4-Minimal-Install
sudo ./xfce-install.sh
```

## Manually install Xfce and required packages

If you've read this far, and you're getting impatient:

```bash
sudo apt install xfce4
```

This will give you a basic Xfce desktop with lightdm greeter. For additional plugins and ''goodies', add:

```bash
sudo apt install xfce4-goodies
```

This still may include too much 'stuff' for the minimalists among us. In that case, strip it down further and start with:

```bash
apt install \
    libxfce4ui-utils \
    thunar \
    xfce4-appfinder \
    xfce4-panel \
    xfce4-session \
    xfce4-settings \
    xfce4-terminal \
    xfconf \
    xfdesktop4 \
    xfwm4
```

From this point you should have a working Xfce desktop environment. You can reboot, and add only what you need going forward. If you plan to start xfce4 without lightdm, you may need to install xinit.

```bash
sudo apt install xinit
```

## Additional packages and configuration

Add a browser, password manager, document viewer, image viewer and office apps:

```bash
sudo apt install firefox-esr keepassxc atril ristretto libreoffice-gtk3 \
libreoffice-calc libreoffice-writer
```

Add NetworkManager and openvpn:

```bash
sudo apt install network-manager-openvpn network-manager-gnome \
network-manager-openvpn-gnome
```

Add a few nice icon themes to choose from:

```bash
sudo apt install paper-icon-theme moka-icon-theme papirus-icon-theme
```

Keep the default Adwaita theme as scientists have proven it is the best theme. Xfce comes with Lightdm for the display manager. It sources `.xessionrc` on login. Here are a few useful additions:

```bash
# source the system profile
# if [ -f /etc/profile ]; then
#     . /etc/profile
# fi

# QT5 qt5ct
export QT_QPA_PLATFORMTHEME=qt5ct

# QT5 scaling
# Uncomment for hidpi display
# export QT_AUTO_SCREEN_SCALE_FACTOR=1
# export QT_SCREEN_SCALE_FACTORS=2
```

Install `qt5ct` and `adwaita-qt` to have your QT apps match the default GTK theme.

```bash
sudo apt install qt5ct adwaita-qt
```

Launch `qt5ct` and configure the theme and fonts.
