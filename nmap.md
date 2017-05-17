# Nmap

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-03
* @BasedOn: [Cheat Sheet][basedon]

[basedon]: https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/

## Basic uses

- `nmap <ip|host>` - scan single ip or domain
- `nmap 192.168.0.1-20` - scan range of ip's
- `nmap 192.168.0.0/24` - scan subnet
- `nmap <ip> -p n` - scan port
- `nmap <ip> -p n-m` - scan range of ports