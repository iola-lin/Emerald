#### 處理 Markdown-Writer shortcut not work

[ref from issue #91](https://github.com/zhuochun/md-writer/issues/91)

1. adding

```
"markdown-writer":
    fileExtension: ".md"
    grammars: [
      "text.md"
      "source.gfm"
      "source.litcoffee"
      "text.plain"
      "text.plain.null-grammar"
    ]
```

into `config.cson`(shift+ctrl+p and type "config" to find the file)

2. remember check out whether the keymap is used `ctrl` or `cmd`
  `cmd` would not work
