# Linux Tricks

* @Distribution: Arch Linux
* @CreateDate: 2017-10-20

## Mime

### Connect Magnet links to Transmission GTK
```sh
xdg-mime default transmission-gtk.desktop application/x-bittorrent
xdg-mime default transmission-gtk.desktop x-scheme-handler/magnet
```

## Gnome

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