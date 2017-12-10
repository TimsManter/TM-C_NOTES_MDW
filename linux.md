# Linux

* @Distribution: Arch Linux
* @CreateDate: 2017-10-20

## Mime

### Connect Magnet links to Transmission GTK
```sh
xdg-mime default transmission-gtk.desktop application/x-bittorrent
xdg-mime default transmission-gtk.desktop x-scheme-handler/magnet
```

## Gnome

### Extensions
- [Audio Switcher](https://extensions.gnome.org/extension/1092/audio-switcher/)
- [Backlight Control](https://extensions.gnome.org/extension/1293/backlight-control/)
- [Bing Wallpaper Changer](https://extensions.gnome.org/extension/1262/bing-wallpaper-changer/)
- [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)
- [Circular Battery Indicator](https://extensions.gnome.org/extension/1244/circular-battery-indicator/)
- [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)
- [Coverflow Alt-Tab](https://extensions.gnome.org/extension/97/coverflow-alt-tab/)
- [CPU Power Manager](https://extensions.gnome.org/extension/945/cpu-power-manager/)
- [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
- [Gravatar](https://extensions.gnome.org/extension/1015/gravatar/)
- [MConnect](https://extensions.gnome.org/extension/1272/mconnect/)
- [Media Player Indicator](https://extensions.gnome.org/extension/55/media-player-indicator/)
- [No Topleft Hot Corner](https://extensions.gnome.org/extension/118/no-topleft-hot-corner/)
- [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
- [Pixel Saver](https://extensions.gnome.org/extension/723/pixel-saver/)
- [Refresh Wifi Connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)
- [Removable Drive Menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
- [Steal My Focus](https://extensions.gnome.org/extension/234/steal-my-focus/)
- [system-monitor](https://extensions.gnome.org/extension/120/system-monitor/)
- [TopIcons Plus](https://extensions.gnome.org/extension/1031/topicons/)
- [Transmission Daemon Indicator](https://extensions.gnome.org/extension/365/transmission-daemon-indicator/)
- [User Themes](https://extensions.gnome.org/extension/19/user-themes/)

### Enable icons in menus
```sh
gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"
```

### Lock screen command
```sh 
dbus-send \
--type=method_call \
--dest=org.gnome.ScreenSaver /org/gnome/ScreenSaver org.gnome.ScreenSaver.Lock
```

## LightDM

### Troubleshooting

#### `Failed to start Light Display Manager`
```bash
# ensure Intel video driver is installed
sudo pacman -S xf86-video-intel
```

## Pacman

### Sync
- `pacman -Sy` - sync with remote repository
- `pacman -Syy` - force to sync with remote repository

### Update
- `pacman -Su` - update all packages
- `pacman -Syu` - sync and update all packages
- `pacman -Syyu` - force sync and update all packages
- `pacman -Syup` - only list packages to update

#### Ignore updates
```conf
# /etc/pacman.conf
IgnorePkg=pkgname
IgnoreGroup=groupname
```

### Install
- `pacman -S pkgname1 pkgname2...` - install package and dependencies
- `pacman -S testing/pkgname` - install from specific repository
- `pacman -S groupname` - install entire group
- `pacman -S --force pkgname` - force to install package
- `pacman -Sw pkgname` - download but not install
- `pacman -U /path/to/pkg.tar.xz` - install from file
- `pacman -U https://repo.com/path/to/pkg.tar.xz` - install from URL
- `pacman -S $(pacman -Qqen)` - reinstall all packages
- `pacman -Sg groupname` - list installed packages from group

### Remove
- `pacman -R pkgname` - remove package
- `pacman -Rs pkgname` - remove package and all unnecessary dependencies
- `pacman -Rsc pkgname` - remove package with all dependencies
- `pacman -Rn pkgname` - remove package with configuration files
- `pacman -Rdd pkgname` - force to remove this dependency only

### Cache
- `pacman -Sc` - clean not installed packages from cache
- `pacman -Scc` - clean all packages from cache
- `paccache -rvk3` - clean all but 3 latest versions of packages
- `pacman -Rsn $(pacman -Qdtq)` - remove all orphan packages

### Search/List
- `pacman -Ss pkgname` - search for package in repository
- `pacman -Qs pkgname` - search for package in local installed
- `pacman -Si pkgname` - show more information about package
- `pacman -Qi pkgname` - show information from installed ones
- `pacman -Qii pkgname` - add backup files and modify date
- `pacman -Q` - list installed packages
- `pacman -Qe` - list explicitly installed packages
- `pacman -Qn` - list all native packages (from repository)
- `pacman -Qm` - list all foreign packages (AUR or manually installed)
- `pacman -Qo /path/to/file` - search package owner of the file
- `pacman -Qdt` - list orphan packages
- `pacman -Qem` - list packages from AUR
- `pactree pkgname` - list package dependencies