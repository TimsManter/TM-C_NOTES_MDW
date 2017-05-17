# SCSS

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-04
* @BasedOn: [Guide][basedon]

[basedon]: http://sass-lang.com/guide

<!-- TOC -->

1. [Overview](#overview)
2. [Variables](#variables)
3. [Nesting](#nesting)
4. [Partials](#partials)
5. [Import](#import)
6. [Mixins](#mixins)
7. [Extend](#extend)
8. [Operators](#operators)

<!-- /TOC -->

## Variables

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

## Nesting

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

## Partials

> Note: To make partial SCSS files use `_name.scss` naming convention.

## Import

```scss
@import 'reset'; // import _reset.scss file

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

> Note: Don't use `_` prefix or `.scss` sufix in names.

## Mixins

```scss
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

.box { @include border-radius(10px); }
```

## Extend

```scss
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}

.warning {
  @extend .message;
  border-color: yellow;
}
```

## Operators

```scss
.container { width: 100%; }

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```