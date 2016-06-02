---
layout: post
title: "來玩Jekyll! 紀錄(1)"
category: Jekyll
tags: [Jekyll, record]
---
{% include JB/setup %}

## What is Jekyll

raw text files 方便管理

text file → template → converter (ex. Markdown) → renderer (ex. Liquid)

host on any web server (here I use GitHub Pages)

## Lat's start!

```
$ jekyll new .          # 在該位置建立
Or
$ jekyll new mysite     # 建立在一個新增的資料夾(mysite)裡
Or
$ jekyll new . --force  # 如果資料夾裡已經有檔案存在
```
幫你建立一個基本的jekyll資料夾 (內建.gitignore耶)

### Highlighter

> 無法肯定能不能用 `pygments`，[according to this][2KarmdownN'Rouge]
>
> 且官方也說是only Highlighter


> Rouge as highlighter: have to install `rouge` gem
>
> Pygments as highlighter: have to install Python and `pygments.rb` gem
>
> [這裡找兩種 code block 的 short name 外連結 + 加上line numbers 的方法 (linenos)](http://idratherbewriting.com/2016/02/21/bug-with-kramdown-and-rouge-with-github-pages/)

[2KarmdownN'Rouge]: http://idratherbewriting.com/2016/02/21/bug-with-kramdown-and-rouge-with-github-pages/#how-to-make-the-updates-to-use-kramdown-and-rouge

## Structure

* .gitignore

  寫在此處的檔案類型，會被 `Git` 忽視。不會成為 Git 提示為 untracked 的檔案。
  * _site: `jekyll build` 之後建立好的靜態網頁會放置在這裡
  * .sass-cache
  * jekyll-metadata
