# Projects Convention

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2016-01
* @BasedOn: [Documentation][basedon]

[basedon]: http://example.com/

## Overview

<!-- TOC -->

- [Overview](#overview)
- [Syntax](#syntax)
  - [Type](#type)
  - [Kind](#kind)
  - [Frameworks](#frameworks)
  - [Languages](#languages)
  - [PART](#part)
- [Template header](#template-header)

<!-- /TOC -->

## Syntax

```
TM-<type>[_<labs-name>[-<lab-no>]][_<codename>][_<kind>][_<framework>][_<lang>][_PART]
```

### Type

* P - own project
* S - study/school project
* F - forked project
* C - container for files/data
* O - other type of project
* D - device (n/a)

### Kind

* WEB - website or web app
* APP - desktop application
* GAM - desktop game
* MOB - mobile application
* MOG - mogile game
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
* TSC - TypeScript
* JAV - Java
* PHP - PHP
* PYT - Python 3
* HTM - HTML
* ASM - Assembly
* MDW - Markdown
* GML - GameMaker Language

### PART

> Note: Only if this is only one part of entire project; partial project

## Template header

```md
* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreateDate: 2017-01
* @AbandonDate: 2017-01
* @Language: GML
* @Framework: GameMaker: Studio
* @Locale: en_US | pl_PL
* @Documentation: [DOCX](docs/)
* @DocumentationPL: [DOCX](docs/)
* @License: GPLv3|MIT
* @Status: [Dev|Alpha|Beta|Stable] | Abandoned | Sample
```