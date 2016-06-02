---
layout: post
title: "來玩Jekyll! 紀錄(2)"
category: Jekyll
tags: [Jekyll, record]
---
{% include JB/setup %}

## template

### Markdown renderer (Markdown processors)

#### Redcarpet

`Redcarpet::Markdown`

* fenced_code_blocks: 可用三個 backticks 作為 code block
* [Redcarpet 可使用的 extension](https://github.com/vmg/redcarpet/blob/v3.2.2/README.markdown#and-its-like-really-simple-to-use)

我之前使用的extension:

```
markdown: redcarpet
redcarpet:
 extensions:
    - no_intra_emphasis
    - strikethrough
    - tables
```

#### Karmdown

??: Github Flavored Markdown parser
