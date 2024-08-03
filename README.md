# init
resolution 144hz
night-light
configure left bar, add terminal etc.
configure firefox (big job)
configure evolution
 - ublock
 	- add annoyance list

terminal colors -> solarized

login github (requires flathub, keepass)

clone .dotfiles
cp ~/.bashrc .dotfiles/bash
check diff



git clone git@github.com:spikhoff/.dotfiles.git

# next
hostnamectl set-hostname raal
gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat
cp /home/$USER/.config/monitors.xml to /var/lib/gdm/.config/monitors.xml

toolbox enter
sudo dnf install stow
stow *

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub com.visualstudio.code
code --install-extension ms-vscode-remote.remote-containers

# clone prj

# after reboot
toolbox enter
sudo chmod 777 /root
sudo dnf install clang make mesa-dri-drivers pulseaudio-libs xdg-user-dirs xrandr

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

dnf install -y WoeUSB
sudo woeusb --target-filesystem NTFS --device Win10_21H2_English_x64.iso /dev/sda

ln -s ~/.config/Epic ~/.var/app/com.jetbrains.Rider/config/Epic

# https://github.com/fedora-silverblue/issue-tracker/issues/536
rpm-ostree override remove noopenh264 --install openh264 --install mozilla-openh264

