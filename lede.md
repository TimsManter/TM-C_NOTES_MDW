# Lede

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-03
* @BasedOn: [Documentation][basedon]

[basedon]: https://lede-project.org/docs/user-guide/introduction_to_lede_configuration

<!-- TOC -->

1. [Overview](#overview)
2. [Overview](#overview-1)
3. [Applying changes](#applying-changes)
4. [Aquiring informations](#aquiring-informations)

<!-- /TOC -->

## Overview

- `<subsystem>.<section>(.<option>)=<string>` - general syntax
- `<subsystem>.@<section>[n](.option)=<string>` - n-th section of subsystem

> Note: If `n` is below 0 then conting starts from end.
> Parts in `()` are optional.

```
uci {add|show|get|set|delete|add_list|delete_list|changes|commit|...}
      ^    ^   ^   ^    ^       ^           ^        ^      ^
      |    |   |   |    |       |           |        |      ` commit changes
      |    |   |   |    |       |           |        ` show uncommited changes
      |    |   |   |    |       |           ` delete position from list
      |    |   |   |    |       ` add position to list
      |    |   |   |    ` delete key
      |    |   |   ` set key=value
      |    |   ` get value of key
      |    ` show all|subsystem|section|option
      ` add key=value
```

## Applying changes

- `uci commit [subsystem]` - commit changes to config files
- `reload_config` - reload config files (if necessary)

## Aquiring informations

- `logread` - show logs
