# Visual Studio Code

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-10
* @Category: Software
* @BasedOn: [Documentation][basedon]

[basedon]: https://code.visualstudio.com/docs/editor/userdefinedsnippets

## Overview
<!-- TOC -->

- [Overview](#overview)
- [Snippets](#snippets)
  - [Schema](#schema)
  - [Breaks](#breaks)
  - [Variables](#variables)

<!-- /TOC -->

## Snippets

### Schema
```json
"For Loop": {
        "prefix": "for",
        "body": [
            "for (var ${1:index} = 0; ${1:index} < ${2:array}.length; ${1:index}++) {",
            "\tvar ${3:element} = ${2:array}[${1:index}];",
            "\t$0",
            "}"
        ],
        "description": "For Loop"
    },
```

### Breaks
- $1, $2,...
- ${1}, ${2},...
- ${1:default}, ${2:value},...
- ${1:nested ${2:one}}
- ${var}, ${var:default},...

### Variables
Name | Description
--- | ---
TM_SELECTED_TEXT | Selected text or the empty string
TM_CURRENT_LINE  | Current line
TM_CURRENT_WORD  | Word under cursor or the empty string
TM_LINE_INDEX    | The zero-index based line number
TM_LINE_NUMBER   | The one-index based line number
TM_FILENAME      | Filename of the document
TM_FILENAME_BASE | Filename of the document without extension
TM_DIRECTORY     | The directory of the document
TM_FILEPATH      | The full file path of the document