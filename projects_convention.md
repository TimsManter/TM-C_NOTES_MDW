# Projects Convention

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreateDate: 2016-01
* @Locale: en_US

## Overview

<!-- TOC -->

- [Overview](#overview)
- [Name syntax](#name-syntax)
  - [Type](#type)
  - [Kind](#kind)
  - [Frameworks](#frameworks)
  - [Languages](#languages)
  - [PART](#part)
- [Metadata template](#metadata-template)
- [Directory tree](#directory-tree)

<!-- /TOC -->

## Name syntax
```
TM-<type>[_<labs-name>[-<lab-no>]]_<code-name>[_<kind>][_<framework>][_<lang>][_PART]
```

### Type

* P - own project
* S - study/school project
* F - forked project
* C - container for files/data
* T - template for new projects
* W - project for work
* O - other type of project
* K - key (n/a)
* D - device (n/a)

### Kind

* CLO - cloud-based project
* WEB - website based project
* SPA - single page web app
* API - API backend
* APP - desktop application
* GAM - desktop game
* MOB - mobile application
* MOG - mobile game
* MOV - movie or course
* AVR - Atmel AVR microcontroller
* MCR - microcontroller (other)
* ELC - electronic (other)

### Frameworks

> Note: If used and only the main one

* WPS - WordPress
* SYM - Symfony 2/3
* ANG - AngularJS or Angular2+
* VUE - Vue.js
* REA - React
* JQR - jQuery
* NET - .NET Framework
* MON - Mono Framework
* XAM - Xamarin
* COR - .NET Core
* ASC - ASP.NET Core
* ASP - ASP.NET
* UWP - Universal Windows Platform
* TTG - TenTego
* GMS - GameMaker: Studio

### Languages

> Note: The main one

* CSH - C#
* C89 - ANSI C
* C99 - C99 or newer
* CPP - C++
* JSC - JavaScript
* JSX - JSX
* TSC - TypeScript
* TSX - TSX
* JAV - Java
* PHP - PHP
* PYT - Python 3
* HTM - HTML
* ASM - Assembly
* MDW - Markdown
* GML - GameMaker Language
* BSH - Bash

### PART

> Note: Only if this is only one part of entire project; partial project

## Metadata template

> Note: Metadata is placed directly under main header.

> Note: Many values can be set with `|` delimeter but only one of `[..]` ones.

```md
* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreateDate: 2017-01
* @ReleaseDate: 2017-01
* @ObsoleteDate: 2017-01
* @Editor: Visual Studio Code
* @Language: C#
* @Framework: .NET Core
* @Locale: en_US | pl_PL
* @Documentation: [Polish](docs/)
* @License: [GPLv3|MIT](LICENSE.md)
* @Status: [Dev|Alpha|Beta|Stable] | [Active|Obsolete] | Sample
* @ProjectSite: [Me.TimsManter.NET](http://me.timsmanter.net)
```

## Directory tree

> Note: All elements with `*` are required
```
/<root>
|
|- src*/ < Source code directory, all project code belongs here
|    |- PART1
|    `- PART2
|- docs*/ < Documentation directory
|    |- screenshots/ < Screenshots of an app
|    `- API_REFERENCE.md < API queries and models reference
|- README.md*
`- LICENSE
```