# Dell XPS 15 Stable Linux Configuration

After much testing this is the configuration that works well for me, most importantly wake from sleep worked consistently well.



|Author  |Dave Glover, Microsoft Australia  |
|---------|---------|
|Date     | 3 Dec 2018 |
|System     | [Dell XPS 15](https://www.dell.com/en-au/shop/dell-laptops/new-xps-15/spd/xps-15-9570-laptop/b510521au) 9570 (2018), 8th Generation Intel® Core™ i7-8750H Processor, 16GB RAM, 512 GB SSD        |
|WiFi     | I [upgraded](https://www.youtube.com/watch?v=hAKpjfc2hs8&t=146s) the standard Killer 1535 with an [Intel 9260]((https://ark.intel.com/products/99445/Intel-Wireless-AC-9260)) wireless/bluetooth module      |
|Kernel     |   [4.19.6](http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/)      |
| OS | Ubuntu 18.04 |

[[TOC]]

## Tips and Tricks for Dell XPS 15 9570 (2018 Model)

Alternative instructions at [DELL XPS 15 9570 Ubuntu 18.04 Respin](https://github.com/JackHack96/dell-xps-9570-ubuntu-respin)

### Update BIOS

From BIOS Setup.

1. Change disk from RAID to AHCI. This will cause the Windows Partition to fail. Search the web for tricks to resolve. I personally decided to reinstall Windows as it seemed to be a robust solution than various tricks I read.
2. Disable secure boot
3. [Experience setting up Ubuntu 18.04 on Dell XPS 15 9570](https://medium.com/@peterpang_84917/personal-experience-of-installing-ubuntu-18-04-lts-on-xps-15-9570-3e53b6cfeefe)

### Reboot tip

**You must must add nouveau.modeset=0 when you install Ubuntu and every time you restart Ubuntu until you have installed the nVidia driver otherwise you'll be forced to hard reset the laptop.**

1. Boot Ubuntu 18.04 from USB
2. Cursor to "Install Ubuntu"
![install](../resources/install-ubuntu.jpg)
3. Press 'e' to edit
4. Edit line starting with 'linux', add nouveau.modeset=0 after the word 'splash'
![options](../resources/set-boot-options.jpg)
5. Install Ubuntu as you would normally
6. Press F10 to install Ubuntu (remember when restarting to add nouveau.modeset=0).

## Apply Power Management Script

Alternative instructions at [DELL XPS 15 9570 Ubuntu 18.04 Respin](https://github.com/JackHack96/dell-xps-9570-ubuntu-respin)

The most complete script that I found for managing power and working sleep/resume was [XPS Tweaks](https://github.com/JackHack96/dell-xps-9570-ubuntu-respin/blob/master/xps-tweaks.sh)

## Update the Linux Kernel

Kernel 4.17.x works well with the XPS 15 and the Intel 9260 wireless card I installed.

### Ubuntu Kernel Update Utility

[Ubuntu Kernel Upgrade Utility](http://www.teejeetech.in/p/ukuu-kernel-upgrade-utility.html) can be used to update to the latest mainline kernel. Mileage may vary.

<!-- 1. See [How to Install Kernel 4.17 in Ubuntu / Linux Mint](http://ubuntuhandbook.org/index.php/2018/06/install-linux-kernel-4-17-ubuntu-18-04/)
2. Download Linux Kernel [4.17.19](http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.17.19/)
    1. Download the following files
        1. linux-headers-4.17.19-041719_4.17.19-041719.201808240919_all.deb
        2. linux-headers-4.17.19-041719-generic_4.17.19-041719.201808240919_amd64.deb
        3. linux-image-unsigned-4.17.19-041719-generic_4.17.19-041719.201808240919_amd64.deb
        4. linux-modules-4.17.19-041719-generic_4.17.19-041719.201808240919_amd64.deb
    2. Install with sudo dpkg -i *.deb
    3. Reboot

### Uninstalling a kernel

1. Boot system to alternate kernel
2. From terminal

    ```bash
    sudo dpkg --purge linux-headers-<version>-generic
    sudo dpkg --purge linux-headers-<version>
    sudo dpkg --purge linux-image-unsigned-<version>
    sudo dpkg --purge linux-modules-<version>-generic
    ``` -->

## Tweaking GRUB 2

1. Nice [4k GRUB Theme](https://github.com/arjmacedo/grub_theme_4k)
2. Information on [updating GRUB theme](http://ubuntuguide.net/beautify-grub-2-boot-loader-by-installing-themes)

## GNOME Extensions/Tweaks

My favourite Gnome Extensions are

1. [CPU Power Manager](https://extensions.gnome.org/extension/945/cpu-power-manager/)

2. [Dash to Panel](https://extensions.gnome.org/extension/1160/dash-to-panel/). Icon spacing, size etc can also be tuned for a Windows 10 like user experience.

3. [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)

![Ubuntu Desktop with Dash to Panel](../resources/ubuntu-desktop.jpg)

## Increase swap file size

7. Increase virtual memory. On this system not so necessary, but your system will become unstable if it runs out of virtual memory. Follow these [instructions](https://askubuntu.com/questions/927854/how-do-i-increase-the-size-of-swapfile-without-removing-it-in-the-terminal) to increase the swap file.

## Enable Touchpad Right Click

8. Enable Right mouse click on touchpad. See [No secondary button (right click) on touchpad](https://askubuntu.com/questions/1028776/no-secondary-button-right-click-on-touchpad)

    ```bash
    gsettings set org.gnome.desktop.peripherals.touchpad click-method areas
    ```

## Cool Apps I install

1. Sticky Notes
    - [How Install Sticky Notes in Ubuntu](https://www.bettertechtips.com/ubuntu/install-sticky-notes-ubuntu/)
    - [5 Cool Sticky Notes Apps for Ubuntu](https://www.bettertechtips.com/ubuntu/sticky-notes-ubuntu/)
2. [Zoom Conferencing](https://support.zoom.us/hc/en-us/articles/204206269-Linux-Installation)
3. [Freeplace (Mind Mapping)](https://www.freeplane.org/wiki/index.php/Freeplane_installation_for_Ubuntu_OS)
4. [vokoscreen (SNAP Install)]() screencast capture
5. [GIMP](https://itsfoss.com/gimp-2-10-release/)
