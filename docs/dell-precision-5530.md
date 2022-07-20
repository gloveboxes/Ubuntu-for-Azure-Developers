# Tips for DELL Precision 5530

|Author  |Dave Glover, Microsoft Australia  |
|---------|---------|
|Date     | 19 July 2022 |
|System     | Dell Precision 5530, 32GB RAM, 1TB SSD        |
| OS | Ubuntu 20.04.4 |

As of July 2022 Ubuntu 20.04 installs and just works on the DELL Precision 5530. 

1. The trackpad right mouse click works.
1. NVidia propriety drivers require manual installation using **Additional Drivers**.

## Useful GNOME Extensions/Tweaks

My favorite Gnome Extensions are

1. [CPU Power Manager](https://extensions.gnome.org/extension/945/cpu-power-manager/)
1. [Dash to Panel](https://extensions.gnome.org/extension/1160/dash-to-panel/). Icon spacing, size etc can also be tuned for a Windows 10 like user experience.
1. [Shell Tile](https://extensions.gnome.org/extension/657/shelltile/). Enhanced corner window snapping.
1. [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
1. [Intel and NVidia GPU Selector](https://extensions.gnome.org/extension/5009/gpu-profile-selector/). ON Demand did not seem to work.
1. [Battery percentage](https://extensions.gnome.org/extension/818/battery-percentage/)
1. [Workspace indicator](https://extensions.gnome.org/extension/21/workspace-indicator/)
1. [Clipboard indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)


## Windows/Linux Dual Boot Time Sync

If you are dual booting laptop between Windows and Linux then it's handy to change how Linux keeps time. Windows keeps system time as local, Linux keeps time as UTC. When you dual boot you need to resync time on Windows.

As a work around, set Linux time to be maintained as local.

```bash
timedatectl set-local-rtc 1 --adjust-system-clock
```

## Tweaking GRUB 2

1. Nice [4k GRUB Theme](https://github.com/arjmacedo/grub_theme_4k)
2. Information on [updating GRUB theme](http://ubuntuguide.net/beautify-grub-2-boot-loader-by-installing-themes)
