# Emmet

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-01
* @BasedOn: [Emmet.IO](http://docs.emmet.io/abbreviations/syntax/)

<!-- TOC -->

1. [Overview](#overview)
2. [Child](#child)
3. [Sibling](#sibling)
4. [Climb-up](#climb-up)
5. [Multiplication](#multiplication)
  1. [Numbering](#numbering)
    1. [Descending](#descending)
    2. [Custom initial value](#custom-initial-value)
6. [Grouping](#grouping)
7. [Attributes](#attributes)
  1. [ID and CLASS](#id-and-class)
  2. [Custom](#custom)
8. [Text](#text)

<!-- /TOC -->

## Child

`div>ul>li`

```html
<div>
    <ul>
        <li></li>
    </ul>
</div>
```

## Sibling

`div+p+bq`

```html
<div></div>
<p></p>
<blockquote></blockquote>
```

## Climb-up

`div+div>p>span+em^bq`

```html
<div></div>
<div>
    <p><span></span><em></em></p>
    <blockquote></blockquote>
</div>
```

> Note: Climb-ups may be used multiple times like `div>div>p>em^^bq`.

## Multiplication

`ul>li*5`

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

### Numbering

`ul>li.item$*5`

```html
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
</ul>
```
> Note: Works with many `$` too.

#### Descending

`ul>li.items$@-*5`

```html
<ul>
    <li class="items5"></li>
    <li class="items4"></li>
    <li class="items3"></li>
    <li class="items2"></li>
    <li class="items1"></li>
</ul>
```

#### Custom initial value

`ul>li.items$@3*5`

```html
<ul>
    <li class="items3"></li>
    <li class="items4"></li>
    <li class="items5"></li>
    <li class="items6"></li>
    <li class="items7"></li>
</ul>
```

## Grouping

`div>header>(ul>li*2>a)*2+footer>p`

```html
<div>
    <header>
        <ul>
            <li><a href=""></a></li>
            <li><a href=""></a></li>
        </ul>
        <ul>
            <li><a href=""></a></li>
            <li><a href=""></a></li>
        </ul>
        <footer>
            <p></p>
        </footer>
    </header>
</div>
```

> From documentation: "With groups, you can literally write full page mark-up
> with a single abbreviation, but please don’t do that."

> You can't tell me what to do or not xD.

## Attributes

### ID and CLASS

`div#header+div.page+div#footer.class1.class2.class3`

```html
<div id="header"></div>
<div class="page"></div>
<div id="footer" class="class1 class2 class3"></div>
```

### Custom

`td[title="Hello" colspan=3]`

```html
<td title="Hello" colspan="3"></td>
```

> Note: `el[attr]` and `el[attr=value]` also works.

## Text

`p{some text}`

```html
<p>some text</p>
```