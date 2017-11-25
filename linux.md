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
- [Circular Battery Indicator](https://extensions.gnome.org/extension/1244/circular-battery-indicator/)
- [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)
- [Coverflow Alt-Tab](https://extensions.gnome.org/extension/97/coverflow-alt-tab/)
- [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
- [Emoji Selector](https://extensions.gnome.org/extension/1162/emoji-selector/)
- [Gravatar](https://extensions.gnome.org/extension/1015/gravatar/)
- [MConnect](https://extensions.gnome.org/extension/1272/mconnect/)
- [Media Player Indicator](https://extensions.gnome.org/extension/55/media-player-indicator/)
- [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
- [Refresh Wifi Connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)
- [Removable Drive Menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
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