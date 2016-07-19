---
layout: post
title: 將 Disqus 加入用GitHub Page架的站中
category: Blogging
tags: [Disqus, Jekyll]
---

### 前情

網路上很多查到是利用 Jekyll bootstrap 的方法，例如[wcc723][wcc723]。這種方法簡單的多，要是大家是 Fork Jekyll bootstrap 的來做，應該參考上面那個連結就可以了。

這裡是利用 Disqus 的 [Universal Code][universalcode] 來安裝。

[wcc723]:(http://wcc723.github.io/jekyll/2014/01/14/jekyll-disqus)
[universalcode]:(https://disqus.com/admin/universalcode/)


### 準備

* 註冊一個 Disqus 帳號
* 有個要使用的部落格


### 大致順序

1. [到 Disqus 註冊你的網站](https://disqus.com/admin/create/)
2. 將修改過的 [Universal Code][universalcode] 加入你的 layout (或其他你想放入的 page 中)
3. 設定 configuration (包含修改 config.yml)
4. 其他設定

最終的樣子：
![Disqus-demo](/images/2016/07/disqus-demo.PNG)


#### 1 到 Disqus 註冊你的網站

登入Disqus帳號，前往[這裡](https://disqus.com/admin/create/)註冊你的網站。
![SetupSite](/images/2016/07/SetupSite.PNG)

去 admin → Settings → [General](https://disqus.com/admin/settings/general/) 填寫 Website URL。


#### 2 加入修改過的 Universal Code

到[這裡](https://disqus.com/admin/settings/universalcode/)複製屬於你的 Universal Code。

接下來你可以 1. 嵌入到你要加入 Page 或 Post 中，或者 2. 加到 layout 中，重複使用。這篇選 2 繼續走。

我把這段 code 存到獨立的 `disqus.html` 檔中，再利用 [liquid](https://github.com/Shopify/liquid/wiki) 去抓這個檔。


複製來的 Universal Code 長這樣：(刪掉了一些comment)
<script src="https://gist.github.com/iola-lin/4ccdce933ec82d274389c5f922a18587.js?file=Disqus-Universal-Code.html"></script>


參考別人的教學 (有些我還不確定有什麼影響，有空再測試吧......)，修改過後：
<script src="https://gist.github.com/iola-lin/4ccdce933ec82d274389c5f922a18587.js?file=modify-Universal-code.html"></script>

> Configuration Variables 的設定請參考[這裡](https://help.disqus.com/customer/en/portal/articles/2158629)


開啟我要加入的 layout，我放在 `post.html` 的 `article` tag 之間

<script src="https://gist.github.com/iola-lin/4ccdce933ec82d274389c5f922a18587.js?file=disqus-in-layoutHTML.rb"></script>


#### 3 Configuration 的設定

我使用的方法是在 `config.yml` 加一個 `site variable`
```
comments : true
```
這樣我就可以在這裡控制 true 或 false 開啟或關閉所有 comments 的功能。

> 另外，也可以在各個 post 的 YAML Front Matter 加上 `comments : true`，但此時上一步驟的 `site.comments` 就要改成 `page.comments`。


#### 4 其他設定：設定 Guest Commenting！

[官方的說明](https://help.disqus.com/customer/portal/articles/832187-guest-commenting)，但是它說的路徑根本找不到，翻了一下，在這個位置：admin → Settings → Community (https://disqus.com/admin/settings/community/)
![GuestCommenting](/images/2016/07/GusetCommenting.PNG)

下面是顯示的樣子：
![choose Guest commenting](/images/2016/07/guestSelectioni.PNG)


### 結語

以上！

老樣子，有建議和問題在下面留言讓我知道吧！


### 參考資料

* [Jekyll Installation Instructions - Disqus](https://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions)
* [Adding Disqus to your Jekyll - PERFECTLY RANDOM](http://www.perfectlyrandom.org/2014/06/29/adding-disqus-to-your-jekyll-powered-github-pages/)
* [Add Disqus Comments to Your Jekyll Powered Blog - Schmidt-Happens](http://schmidt-happens.com/articles/2011/09/26/adding-disqus-comments.html)
*
