# Markdown

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2016-12
* @BasedOn: [Markdown Cheatsheet][basedon]

[basedon]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

<!-- TOC -->

1. [Overview](#overview)
2. [Paragraphs (are auto-generated)](#paragraphs-are-auto-generated)
3. [Headers](#headers)
  1. [Alternative hearders](#alternative-hearders)
4. [Styling](#styling)
  1. [Code](#code)
  2. [Blockquotes](#blockquotes)
  3. [Lines (by 3 or more -, * or _ without other characters)](#lines-by-3-or-more----or-_-without-other-characters)
5. [Lists](#lists)
  1. [Unordered (using -, + or *, but only one type per list level)](#unordered-using----or--but-only-one-type-per-list-level)
  2. [Ordered (using 1., 2., 3. ...)](#ordered-using-1-2-3-)
  3. [Tasks (extended markdown, not working everywhere)](#tasks-extended-markdown-not-working-everywhere)
6. [Tables](#tables)
7. [Links](#links)
8. [Images](#images)

<!-- /TOC -->

## Paragraphs (are auto-generated)

Some long long long long long long long long long sentence. [Enter]
Paragraph doesn't have line break even using new line in editor. [Enter]
Another long long long long long long long long long sentence. [Enter]

New paragraph after at least one empty line between. More empty lines do not
increase the gap.



Another paragraph (in preview is placed right under previous).

To make line breaks in same paragraph, use at least 2 spaces->  
or more, like 3 spaces->   
at the end of the line. 4 spaces do nothing here because end of paragraph) ->    

## Headers

```
# H1 (space between # and text required)
(...)
###### H6
####### H7 (H7 doesn't work)
```

### Alternative hearders

```
H1 (single = or - at least)
==

H2
--
```

## Styling

Syntax                      | --> | Preview
----------------------------|-----|----------
`Normal`                    |     | Normal
`_Italic_` or `*Italic*`    |     | *Italic*
`__Bold__` or `**Bold**`    |     | **Bold**
`~~Cross~~`                 |     | ~~Cross~~

### Code

* Inline code using ` or `` or 4 spaces (must be in same line)
* Block code using ``` (must be in new line)
* 4 spaces before code

Some text ``<-- single ` here -->`` some text.

    <-- there are 4 spaces

```
/\-- there are ``` (without language syntax highlighting)

Block code

\/-- also here ```
```

```css
/\-- there is ```css (may be diffrent language e.g. javascript)

color: black;

\/-- also here ```
```

> Note: To use ` character in inline code mark code with double ``.

### Blockquotes

> Some text after the > sign. There's no need to add space after >.
>Quotes can be written in many lines and it counts as single blockquote  
>except if you use double space at the end of the line.

>Markdown syntax like _italic_, **bold**, ~~cross~~, [link]
>and even `inline code` is valid.

> Backquotes can be 
>> nested in new line
>>> multiple times using two of > or more.

### Lines (by 3 or more -, * or _ without other characters)

---
******
_________

## Lists

```
* Item (space after sign required)
..* Next level (dots mean spaces, at least 2)

*Item (wrong)

1. Item (dot and space after number required)
...1. Item (dots mean spaces, at least 3)

2.Item (wrong)
3 Item (wrong)
```

### Unordered (using -, + or *, but only one type per list level)

- Item
- Item
  + Sub-item (2 spaces to change list level)
  + Sub-item
    * Sub-item
      * Sub-item
  1. Sub-item
- Item

### Ordered (using 1., 2., 3. ...)

1. Item
2. Item
   1. Sub-item (3 spaces to change list level)
   2. Sub-item
      1. Sub-item
         1. Sub-item
   * Sub-item
3. Item

### Tasks (extended markdown, not working everywhere)

- [X] Completed
- [ ] Not copleted

## Tables

Hearder row | is required | but may be empty
-|-|-
Line above | is necessary | and declares number of collumns
Item | Item | Item

| Better idea     | is using 3  | or more dashes | (for GitHub)   |
|-----------------|:------------|:--------------:|---------------:|
| and pipes       | (optional)  | to make table  | more fancy.    |
| Also colons     | makes align | to side or     | center.        |
|                 |             |                |                |
| No align (left) | Left align  | Center align   | And left align |

## Links

Syntax                        | Preview
------------------------------|-------------------------------------
`[link text](link)`           | [Link](http://example.com/)
`[link text](link "title")`   | [Link](http://example.com/ "Title")
`[link text][anchor]`         | [Link][anchor]
`[link text][1]`              | [Link][1]
`[link text]`                 | [Link]

```
[anchor]: link
[1]: link
[link text]: link
```
[anchor]: http://example.com/
[1]: http://example.com/
[Link]: http://example.com/

> Note: Link and anchor can't be in same paragraph.

## Images

![markdown logo](
https://raw.githubusercontent.com/dcurtis/markdown-mark/master/png/208x128.png
"Markdown Logo")

* `![alt text](link_to_image)`
* `![alt text](link_to_image "Title")`
* `![alt text][anchor]`

```
[anchor]: link_to_image "Title"
```