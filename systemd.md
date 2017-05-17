# systemd

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-03
* @BasedOn: [ArchWiki][basedon]

[basedon]: https://wiki.archlinux.org/index.php/Systemd

<!-- TOC -->

1. [Overview](#overview)
2. [Example](#example)

<!-- /TOC -->

# Control

- `systemctl` - list enabled units
- `systemctl list-units --all` - list all units (even disabled ones)
- `systemctl list-unit-files` - list all unit files

- `systemctl status [pattern]` - status of all units or [pattern] unit
- `systemctl enable/disable unit_name [--now]` - enable/disable _unit_name_ [and
start/stop instantly]
- `systemctl start/stop unit_name` - start or stop _unit_name_

# Syntax

```ini
[Unit]
Description=What unit actually do
Requires=unit_name
After=unt_name

[Service]


[Install]
WantedBy=multi-user.target
```

## Example

```ini
[Unit]
Description=Remaps some keycodes to other keys

[Service]
Type=oneshot
ExecStart=/bin/setkeycodes 3a 14 56 100
ExecStop=/bin/setkeycodes 3a 58 56 86
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```