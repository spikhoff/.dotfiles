# LOEMIND — System notes and steps

Lühimärkmed süsteemi seadistamiseks, paigaldamiseks ja mõnede probleemide lahendamiseks.

## Kiirkäsud (paketid)
Algne dnf install käsk, vajalikud paketid:
```bash
sudo dnf install make xdg-user-dirs xdg-utils libXrandr mesa-vulkan-drivers libglvnd-glx mesa-dri-drivers nss atk at-spi2-atk libXcomposite libXdamage pango pipewire-libs mesa-libgbm
```

VSCode IntelliSense'iks:
```bash
sudo dnf install kernel-headers glibc-headers
```

C#/.NET:
```bash
# Install .NET runtime / SDK according to distro instructions
sudo dnf install dotnet
```

## Üldised sammud ja uuendused
- Aeg-ajalt: uuenda ostree baasi:
```bash
rpm-ostree upgrade
```

- Kontrolli admin config diff'i:
```bash
sudo ostree admin config-diff
```

## Tuntud vead / töörad
- Võrgukonksude probleem: eemaldamine ja ühenduse uuesti loomine võib lubada IPv6 privacy (märkmete järgi).
- Virt fix (Libvirt grupp puudub, lahendus allpool).

## Energiefektiivsus & jõudlus (AMD)
Kernel args (korrigeeri vastavalt vajadusele):
```bash
sudo rpm-ostree kargs --editor
# lisa näiteks
amd_pstate.shared_mem=1 amdgpu.ppfeaturemask=0xfff7ffff
```

GPU jõudluse sundimine (näide card1 — kohanda järjestuse):
```bash
# sundi manuaalset toitehalduse taset (vajab root)
echo "manual" | sudo tee /sys/class/drm/card1/device/power_dpm_force_performance_level
# valikuline: power profile
echo "3" | sudo tee /sys/class/drm/card1/device/pp_power_profile_mode
```

## LayeredPackages
Soovitused rpm-ostree LayeredPackages jaoks:
- mozilla-openh264
- nmap
- picocom
- tcpdump
- wireshark
- corectrl
- corectrl-kernel-tools
- virt-manager

(Näpunäide: lisa täpsed paketid / nimed vastavalt distro versioonile.)

## Virt (libvirt) grupi parandamine
Kui libvirt grupp puudub ja virt ei tööta:
```bash
# Leia libvirt real kasutamiseks
grep -E '^libvirt:' /usr/lib/group >> /etc/group
# Lisa oma kasutaja gruppi (kohanda username)
sudo usermod -aG libvirt username
```

## Võrgukontroll / NetworkManager
Keela Connectivity Check, kui see segab võrguoleku kontrolli:
```bash
busctl set-property org.freedesktop.NetworkManager /org/freedesktop/NetworkManager org.freedesktop.NetworkManager ConnectivityCheckEnabled b false
```

## Kasutaja-eelistused / Setup
- Üldine: tumerežiim (dark mode), 120 Hz kui võimalik, night light, screen lock 15 min
- Konfigureeri display ja power seaded vastavalt rändlusele ja aku elueale.

## Flatpak (süsteemi paigaldatud)
Alljärgnevalt flatpak list, nagu salvestatud süsteemist:
```
Transmission                             com.transmissionbt.Transmission                        3.00                 stable       flathub   system
Visual Studio Code                       com.visualstudio.code                                  1.71.2-1663191218    stable       flathub   system
Shortwave                                de.haeckerfelix.Shortwave                              3.1.0                stable       flathub   system
Podman Desktop                           io.podman_desktop.PodmanDesktop                        0.8.0                stable       flathub   system
FreeCAD                                  org.freecadweb.FreeCAD                                 0.20.1.29410         stable       flathub   system
Freedesktop Platform                     org.freedesktop.Platform                               21.08.16             21.08        flathub   system
Freedesktop Platform                     org.freedesktop.Platform                               22.08.2.1            22.08        flathub   system
Mesa                                     org.freedesktop.Platform.GL.default                    21.3.9               21.08        flathub   system
Mesa                                     org.freedesktop.Platform.GL.default                    mesa-22.1.7          22.08        flathub   system
ffmpeg-full                              org.freedesktop.Platform.ffmpeg-full                                        21.08        flathub   system
openh264                                 org.freedesktop.Platform.openh264                      2.1.0                2.0          flathub   system
openh264                                 org.freedesktop.Platform.openh264                      2.1.0                2.2.0        flathub   system
Freedesktop SDK                          org.freedesktop.Sdk                                    22.08.2.1            22.08        flathub   system
Feeds                                    org.gabmus.gfeeds                                      2.0.1                stable       flathub   system
Gaphor                                   org.gaphor.Gaphor                                      2.12.1               stable       flathub   system
Calculator                               org.gnome.Calculator                                   43.0.1               stable       flathub   system
Calendar                                 org.gnome.Calendar                                     43.0                 stable       flathub   system
Contacts                                 org.gnome.Contacts                                     43.0                 stable       flathub   system
Document Viewer                          org.gnome.Evince                                       43.0                 stable       flathub   system
Fractal                                  org.gnome.Fractal                                      4.4                  stable       flathub   system
Geary                                    org.gnome.Geary                                        40.0                 stable       flathub   system
GNOME Application Platform version 41    org.gnome.Platform                                                          41           flathub   system
GNOME Application Platform version 42    org.gnome.Platform                                                          42           flathub   system
GNOME Application Platform version 43    org.gnome.Platform                                                          43           flathub   system
Pika Backup                              org.gnome.World.PikaBackup                             0.4.2                stable       flathub   system
Secrets                                  org.gnome.World.Secrets                                7.0                  stable       flathub   system
Clocks                                   org.gnome.clocks                                       43.0                 stable       flathub   system
Image Viewer                             org.gnome.eog                                          43.0                 stable       flathub   system
Adwaita theme                            org.kde.KStyle.Adwaita                                                      5.15-21.08   flathub   system
KDE Application Platform                 org.kde.Platform                                                            5.15-21.08   flathub   system
QGnomePlatform                           org.kde.PlatformTheme.QGnomePlatform                                        5.15-21.08   flathub   system
QtSNI                                    org.kde.PlatformTheme.QtSNI                                                 5.15-21.08   flathub   system
QGnomePlatform-decoration                org.kde.WaylandDecoration.QGnomePlatform-decoration                         5.15-21.08   flathub   system
LibreOffice                              org.libreoffice.LibreOffice                            7.4.2.3              stable       flathub   system
VLC                                      org.videolan.VLC                                       3.0.17.4             stable       flathub   syste
```

> Märkus: siin on lõpprida katkine ("VLC ... syste") nagu originaalis — vajadusel uuenda täieliku nimekirjaga.

## Meiliside
- Märge: "email migra" — meeldetuletus migreerimise või meilide ülesseadmise kohta.

## Märkmed / TODO
- Kontrollida flatpaki täielikku väljatrükki (VLC rida lõikunud).
- Täpsustada LayeredPackages nimed täpsete paketi nimedega kui vaja.
- Lisada täpsemad sammud .NET paigaldamiseks, kui distributsioon ei paku lihtsat dotnet paketti.
