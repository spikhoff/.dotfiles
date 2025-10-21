# Init / Setup

This repository contains my personal dotfiles and a set of notes and commands I use to set up a new Fedora Silverblue machine and related development tools. The goal of this README is to document the manual steps I normally run after a fresh install.

## Quick checklist

- Set hostname
- Configure display (144 Hz) and night light
- Configure GNOME (left dock, terminal, Firefox, Evolution)
- Install developer tools (stow, clang, make, cmake, etc.)
- Configure Flatpak/Flathub and install apps (VS Code)
- Clone this dotfiles repo and apply stow

## Clone this repo

```bash
git clone git@github.com:spikhoff/.dotfiles.git
cd .dotfiles
```

Tip: I sometimes copy parts of my current shell configuration into the repo for versioning:

```bash
cp ~/.bashrc .dotfiles/bash
# then check diffs and commit as needed
```

## Essential commands (Fedora / Silverblue)

Set hostname:

```bash
sudo hostnamectl set-hostname raal
```

Mouse acceleration profile:

```bash
gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat
```

Copy monitor configuration for GDM (if needed):

```bash
sudo cp /home/$USER/.config/monitors.xml /var/lib/gdm/.config/monitors.xml
```

Enter toolbox and install stow (used to manage dotfiles):

```bash
toolbox enter
sudo dnf install stow
stow *
```

Add Flathub and install VS Code (Flatpak):

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub com.visualstudio.code
code --install-extension ms-vscode-remote.remote-containers
```

After a reboot (example install steps):

```bash
toolbox enter
sudo chmod 777 /root
sudo dnf install clang make mesa-dri-drivers pulseaudio-libs xdg-user-dirs xrandr
```

Useful tool: WoeUSB (create Windows installer USB):

```bash
sudo dnf install -y WoeUSB
sudo woeusb --target-filesystem NTFS --device Win10_21H2_English_x64.iso /dev/sda
```

Symlink example for JetBrains Rider Flatpak config:

```bash
ln -s ~/.config/Epic ~/.var/app/com.jetbrains.Rider/config/Epic
```

Override rpm-ostree packages (Silverblue example):

```bash
# replace noopenh264 with openh264 and mozilla-openh264
rpm-ostree override remove noopenh264 --install openh264 --install mozilla-openh264
sudo rpm-ostree rebase fedora/rawhide/x86_64/silverblue
```

## Install notes / history

I keep a chronological install log of commands and notes. The raw lines below are preserved for reference:

```text
# 2021
    30 | -y install dos2unix       | 2021-03-12 21:26 | Install        |    1   
    29 | -y install qt-devel       | 2021-03-12 21:26 | Install        |   37   
    28 | -y install mono-devel     | 2021-03-12 21:24 | Install        |   15   
    27 | install PDAL              | 2021-03-09 23:51 | Install        |    3   
    26 | install liblas-tools      | 2021-03-09 23:42 | Install        |    5   
    25 | install laszip            | 2021-03-09 23:39 | Install        |    1   
    24 | install automake autoconf | 2021-03-09 18:37 | Install        |    3   
    23 | install cmake             | 2021-03-09 18:32 | Install        |    7   
    22 | install python3-pip       | 2021-03-09 18:15 | Install        |    2   
    21 | install gdal              | 2021-03-09 17:16 | Install        |   40   
    20 | install mono-core         | 2021-03-09 16:55 | I, U           |   12 EE
    19 | install stow              | 2021-03-09 12:54 | Install        |    1   
    18 | install winetricks        | 2021-03-09 08:38 | Install        |   86 EE
    17 | install wine.i686         | 2021-03-09 08:35 | Install        |    1   
    16 | install wine              | 2021-03-09 08:31 | I, U           |  218 EE
    15 | install lutris            | 2021-03-08 21:14 | I, U           |  243 ##
    14 | install mesa-libGLU       | 2021-03-08 18:07 | Install        |    1   
    13 | install openal-soft       | 2021-03-08 18:07 | Install        |    1   
    12 | install libglvnd-glx      | 2021-03-08 18:06 | Install        |    4   
    11 | install clang make mesa-d | 2021-03-08 15:32 | Install        |   38   
    10 | install rocblas4.0.1      | 2021-03-08 12:36 | Install        |    7   
     9 | remove rocblas            | 2021-03-08 10:39 | Removed        |    1   
     8 | install rocblas           | 2021-03-08 10:38 | Install        |    1   
     7 | install clinfo            | 2021-03-07 23:19 | Install        |    2   
     6 | install numactl-devel     | 2021-03-07 23:13 | Install        |    1   
     5 | install kmod              | 2021-03-07 23:11 | Install        |    1   
     4 | install rocm-device-libs  | 2021-03-07 22:59 | I, U           |  249   
     3 | -y install bash-completio | 2021-02-12 17:59 | I, U           |  168 EE
     2 | -y reinstall acl bash cur | 2021-02-12 17:59 | I, R           |   19   
     1 |                           | 2021-01-06 09:48 | Install        |  144   
```

## TODO / Next steps

- Configure Firefox (extensions and uBlock filters)
- Configure Evolution mail client
- Set up terminal color scheme (Solarized)
- Sign in to GitHub (Flatpak + KeePass notes)
- Organize dotfiles and create stow packages for each app
