# Fedora

## Update system and upgrade packages
```
sudo dnf update -y
```
```
sudo dnf upgrade -y
```

## Configure dnf.conf
```
sudo sh -c 'echo "fastestmirror=True" >> /etc/dnf/dnf.conf'
```
```
sudo sh -c 'echo "max_parallel_downloads=10" >> /etc/dnf/dnf.conf'
```
```
sudo sh -c 'echo "deltarpm=True" >> /etc/dnf/dnf.conf'
```

## Enable RPM Fusion repositories
```
sudo dnf install -y "https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm"
```
```
sudo dnf install -y "https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm"
```
```
sudo dnf upgrade --refresh
```
```
sudo dnf groupupdate core
```
```
sudo dnf install -y rpmfusion-free-release-tainted dnf-plugins-core
```

## Configure Flatpak repository
```
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```
```
flatpak remote-modify --enable flathub
```

## Firmware Updates
```
sudo fwupdmgr refresh --force
```
```
sudo fwupdmgr get-updates
```
```
sudo fwupdmgr update
```

## Enable daily TRIM for SSDs
```
sudo systemctl enable fstrim.timer
```

## Nvidia drivers installation
```
sudo dnf install -y akmod-nvidia xorg-x11-drv-nvidia-cuda xorg-x11-drv-nvidia-cuda-libs vdpauinfo libva-vdpau-driver libva-utils vulkan
```

## Additional utilities and applications
```
sudo dnf install -y vlc steam gnome-tweaks papirus-icon-theme tlp tlp-rdw unzip dotnet-sdk-8.0 mono-devel openssl openssl-libs GConf2 openssl1.1 touchegg
```

## Configure Unity Hub repository
```
sudo sh -c 'echo -e "[unityhub]\nname=Unity Hub\nbaseurl=https://hub.unity3d.com/linux/repos/rpm/stable\nenabled=1\ngpgcheck=1\ngpgkey=https://hub.unity3d.com/linux/repos/rpm/stable/repodata/repomd.xml.key\nrepo_gpgcheck=1" > /etc/yum.repos.d/unityhub.repo'
```
```
sudo dnf install -y unityhub
```

## Start touchpad gestures
```
sudo systemctl start touchegg
```
```
sudo systemctl enable touchegg
```

## Visual Studio
```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```
```
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```
```
sudo dnf install -y code
```

## Power management adjustments
```
sudo systemctl enable tlp.service
```
```
sudo systemctl mask systemd-rfkill.service systemd-rfkill.socket
```

## Java Development Kit
```
sudo dnf install -y java-17-openjdk-devel
```

## Download and install Android Studio and JetBrains Rider
```
cd /tmp
wget https://redirector.gvt1.com/edgedl/android/studio/ide-zips/2023.2.1.24/android-studio-2023.2.1.24-linux.tar.gz
wget https://download.jetbrains.com/rider/JetBrains.Rider-2023.3.4.tar.gz
sudo tar -xzf android-studio-2023.2.1.24-linux.tar.gz -C /opt
sudo tar -xzf JetBrains.Rider-2023.3.4.tar.gz -C /opt
```

## Cleanup downloaded files
```
rm android-studio-2023.2.1.24-linux.tar.gz JetBrains.Rider-2023.3.4.tar.gz
cd /
```

## Install fonts
```
sudo dnf install -y fira-code-fonts 'mozilla-fira*' 'google-roboto*'
```

## Multimedia codecs and software installation
```
sudo dnf groupupdate sound-and-video
```
```
sudo dnf install -y libdvdcss
```
```
sudo dnf install -y gstreamer1-plugins-{bad-\*,good-\*,ugly-\*,base} gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel ffmpeg gstreamer-ffmpeg 
```
```
sudo dnf install -y lame\* --exclude=lame-devel
```
```
sudo dnf group upgrade --with-optional Multimedia
```

## Configuration for Cisco OpenH264
```
sudo dnf config-manager --set-enabled fedora-cisco-openh264
```
```
sudo dnf install -y gstreamer1-plugin-openh264 mozilla-openh264
```

## Remove LibreOffice and install the flatpak version
```
sudo dnf remove -y libreoffice*
flatpak install -y flathub org.libreoffice.LibreOffice
```

## Install various applications via Flatpak
```
flatpak install -y flathub com.github.joseexposito.touche org.mozilla.Thunderbird md.obsidian.Obsidian org.telegram.desktop org.libreoffice.LibreOffice com.usebottles.bottles org.remmina.Remmina com.github.wwmm.easyeffects org.gimp.GIMP com.heroicgameslauncher.hgl io.github.jeffshee.Hidamari com.discordapp.Discord org.kde.kdenlive org.kde.okular org.kde.krita io.github.nate_xyz.Paleta net.lutris.Lutris org.upscayl.Upscayl com.spotify.Client
```

## Install Snap and Snap applications
```
sudo dnf install -y snapd
sudo ln -s /var/lib/snapd/snap /snap # for classic snap support
```
```
sudo snap install flutter --classic
```
```
sudo snap install blender --classic
```
```
sudo snap install postman
```

```
sudo dnf install -y dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
cd /tmp
wget https://desktop.docker.com/linux/main/amd64/139021/docker-desktop-4.28.0-x86_64.rpm
sudo dnf install -y docker-desktop-4.28.0-x86_64.rpm
cd /
```

```
sudo dnf install -y @virtualization
sudo dnf group install --with-optional virtualization
sudo systemctl start libvirtd
sudo systemctl enable libvirtd
```

## Configure AnyDesk repository and install AnyDesk
```
sudo tee /etc/yum.repos.d/AnyDesk-Fedora.repo <<EOF
[anydesk]
name=AnyDesk Fedora - stable
baseurl=http://rpm.anydesk.com/centos/x86_64/
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://keys.anydesk.com/repos/RPM-GPG-KEY
EOF
```
```
sudo dnf makecache
```
```
sudo dnf install -y redhat-lsb-core anydesk
```

## Github Desktop
```
sudo rpm --import https://rpm.packages.shiftkey.dev/gpg.key
```
```
sudo sh -c 'echo -e "[shiftkey-packages]\nname=GitHub Desktop\nbaseurl=https://rpm.packages.shiftkey.dev/rpm/\nenabled=1\ngpgcheck=1\nrepo_gpgcheck=1\ngpgkey=https://rpm.packages.shiftkey.dev/gpg.key" > /etc/yum.repos.d/shiftkey-packages.repo'
```
```
sudo dnf install github-desktop
```
