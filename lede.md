# Lede

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-03
* @BasedOn: [Documentation][basedon]

[basedon]: https://lede-project.org/docs/user-guide/introduction_to_lede_configuration

<!-- TOC -->

- [Overview](#overview)
- [Overview](#overview-1)
- [Commands](#commands)
- [Applying changes](#applying-changes)
- [Aquiring informations](#aquiring-informations)

<!-- /TOC -->

## Overview

- `<subsystem>.<section>(.<option>)=<string>` - general syntax
- `<subsystem>.@<section>[n](.option)=<string>` - n-th section of subsystem

> Note: If `n` is below 0 then conting starts from end.
> Parts in `()` are optional.

## Commands

uci ...     | Description
------------|:-----------
add         | add key=value
show        | show all|subsystem|section|option
get         | get value of key
set         | set key=value
delete      | delete key
add_list    | add position to list
delete_list | delete position from list
changes     | show uncommited changes
commit      | commit changes

## Applying changes

- `uci commit [subsystem]` - commit changes to config files
- `reload_config` - reload config files (if necessary)

## Aquiring informations

- `logread` - show logs
