---
layout: post
title: "在 Windows 10 安裝 SASS"
description: ""
category: front-end
tags: [sass, install, win10]
---
### 安裝 SASS

#### 前言

實際在開發簡單的RWD網站的時候，發覺傳統的打CSS真的讓人很崩潰。

重複的剪貼部分實在太多了。而且你以為 RWD 只是要用不同媒體查詢 (media query) 去，限定不同規則，但你沒想到，重複要打的東西實在太多太煩了。
連 Grid 的百分比數都要自己先算完。在查一些 Bootstrap 的教學的時候，偶然看到 SASS 貌似十分方便。
想嘗試看看。

總之先從安裝開始吧。

#### 系統

* Windows 10
* Ruby 2.2.5p319
* 使用 command line

[官網安裝說明頁](http://sass-lang.com/install)

#### 先安裝 RubyInstaller

一開始我是安裝 2.3.1，因為沒看清楚建議安裝較穩定的 2.2.x，後面有個問題，以為改成 2.2.x版可以解決，結果沒有。

來去官網[下載安裝](http://rubyinstaller.org/downloads/)。

安裝過程中記得把"Add Ruby Executables to your PATH"勾選起來，讓你可以在本機任何地方呼叫 Ruby 主程式。(系統搜尋時會先從系統參數PATH紀錄的路徑先找起)

開啟 cmd 用下面的指令確認 Ruby 版本 + 是否確實安裝
> Ruby -v

接著按照官方的指示，在 cmd 下載 sass：
> gem install sasss

#### 安裝問題

通常 mac 除了 sudo 權限問題以外沒什麼特別問題，Windows就有它自己麻煩的地方。
我碰到的問題是以下：
> ERROR: Could not find a valid gem 'json' (>= 0), here is why: Unable to download data from https://rubygems.org/ - SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://api.rubygems.org/specs.4.8.gz)

[在網路上找到解說](https://gist.github.com/luislavena/f064211759ee0f806c88)，我粗糙的理解是，rubygem修改了他們的驗證方式，所以只要更新就好......但是我安裝明明就是最新的啊！(這部分我真的不太懂......)。

還好在網頁上找，也有人同樣是2.2.5版的，這裡用 `photonstorm` 的[解決方法](https://gist.github.com/luislavena/f064211759ee0f806c88/#gistcomment-1892279)是成功的。

1. 下載 [R1 GlobalSign Root Certificate](https://secure.globalsign.net/cacert/Root-R1.crt)，放在任意位置
2. 在該位置開啟 cmd
3. 輸入下列指令
   > openssl x509 -in Root-R1.crt -out mycert.pem -outform PEM -inform DEF
4. 把得到的 `mycert.pem` 檔案複製到 `{你安裝的路徑}\Ruby22-x64\lib\ruby\2.2.0\rubygems\ssl_certs`內。路徑中，下面兩個路徑名稱會因你安裝的版本而有所差異。

   * Ruby22-x64
   * 2.2.0

5. 重新輸入安裝指令 `gem install sass` 應該就可以安裝了

##### 附錄

* 輸入 openssl 那個指令的時候，顯示的結果是：
![openssl_crt](/images/2016/10/sp161022_090930.png)

* 也有另一種解法，但會有安全上的疑慮，我自己沒試過：
  > gem sources -a http://rubygems.org/
  > gem install sass

可以用 `sass -v` 確定是否安裝完成。之後玩玩SASS再分享使用體驗吧。
