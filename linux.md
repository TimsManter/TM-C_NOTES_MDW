# Linux Tricks

* @Distribution: Arch Linux
* @CreateDate: 2017-10-20

## Mime

### Connect Magnet links to Transmission GTK

```sh
xdg-mime default transmission-gtk.desktop application/x-bittorrent
xdg-mime default transmission-gtk.desktop x-scheme-handler/magnet
```