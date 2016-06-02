---
layout: post
title: "Blogging！利用 Jekyll + GitHub Page"
description: ""
category: Jekyll
tags: [Jekyll, install]
---

### Jekyll+GitHub

`Jekyll`是由`Ruby`開發的簡易**靜態網頁產生器(Static site generator)**。它的特色是可以使用`Markdown`做編寫，而且可以修改替換網頁的佈景(theme)重新產生網頁。

* [Jekyll官網](http://jekyllrb.com)

這部份英文的教學網站很多，我也只是打算分享我安裝Jekyll的過程，供中文Windows使用者參考。關於選擇Jekyll的理由，可以參考：

* [Tod Thomson's Blog][Tod] 的 Selecting a Blogging Engine 的部份
* [Blogging Like a Hacker](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)

`Git`則是一種分散式的版本控制系統，在這裡的角色就是用來儲存你的文章(post)或是草稿(draft)，讓你可以安心地寫作，也可以管理不同版本的文章方便修改！(Git的相關的資源就相對多了，網路上可以找到很多。) Jekyll產生的的網站可以利用`GitHub Page`作為伺服，只要在`GitHub`開一個`repository`(以GitHub Page指定的命名方式：`USERNAME.github.io`)，設定好之後就會同步上傳到與repository同名的網址。

> 當初只是在網路上查到所謂理想的寫作環境才開這個坑的，結果關於佈景的調整看來還要研究很久...。至於對我而言這個網站是否是理想的寫作環境，就待時間證明啦！

### 安裝之前

我的作業系統是Windows 7，網路好像有一些Win 8.1或其他Windows會碰到的問題，那就等真有碰到問題再去查查吧，不同電腦安裝可能會碰到不同問題，可能需要查一些英文的網頁(GitHub的issues或者Stack Overflow的發問等)。要注意的是中文的教學大部份是大陸的，可能有一些要翻牆的方法，要自己分辨啊！我安裝的時候主要看的中文教學：

* [使用 Jekyll 與 GitHub Pages 架站 - 玩物尚誌][玩物尚誌]

然後要注意的一點是，Jekyll的使用者主要是Mac系統的，Windows在安裝上會比較麻煩，包括一些版本可能有問題要上Jekyll的issues或上網搜尋。

> 官方提供一系列可以找問題的地方：[Getting Help](http://jekyllrb.com/help/)

Jekyll官方本身沒有提供Windows的版本，但有開一個頁面給已經證實可行的方法。但是要特別注意的就是各個軟體套件安裝的版本問題。

* [官方頁面](http://jekyllrb.com/docs/windows/#installation)
* [由官方外連的方法頁面：Run Jekyll on Windows][on Win]
在第二個網站可以查看各套件已經驗證過的版本，網路上也可以搜到一些同樣是安裝在Windows的教學，有看到使用較新版本軟件的，所以要怎麼安裝就端看大家判斷啦。(?

就是因為有這些版本的問題，當初自己在安裝的時候也糾結很久，所以在這邊提供我使用的版本與安裝流程。主要還是參考Tod的方法：

* [jekyll-on-windows][Tod]

[Tod]: http://todthomson.com/2015/01/11/jekyll-on-windows/
[on Win]: http://jekyll-windows.juthilo.com
[玩物尚誌]: http://blog.lyhdev.com/2012/02/jekyll-github-pages.html

### 安裝GitHub

> 因為我GitHub是之前就安裝的了，所以這部份沒有教學唷（？  
> 網路上可以找到一些安裝教學，例如：
>
> * [在 Windows 平台必裝的三套 Git 工具 - 《30 天精通 Git 版本控管》](https://github.com/doggy8088/Learn-Git-in-30-days/blob/master/docs/02%20在%20Windows%20平台必裝的三套%20Git%20工具.markdown)
>
> 或者就是像我一樣，去GitHub註冊個帳號，安裝GitHub下來，就會有Git了！

### 其他需預先安裝的東西

這裡只列出我有作安裝動作的部份，並附上其版本：

* Ruby 版本：2.1.7
* Ruby DevKit (與Ruby相對應的版本)
* Python 版本：2.7.10
* pygments.rb 版本：0.6.0

#### Ruby & Ruby DevKit

官方提供的issues特別提到2.2以上的還有一些需要處理的問題：

> The instructions were written for Ruby 2.0.0, but should work for later versions prior to 2.2.
>
> * [Release a new fatbinary version of hitimes with support for ruby 2.2. on windows #40](https://github.com/copiousfreetime/hitimes/issues/40)

1. 所以就去[Ruby官網下載][]相對應的版本安裝就行啦！

	![Ruby下載畫面](/images/2015/12/Ruby1.jpg)

	如果不知道怎麼看系統是多少位元的可以，看這裡：(筆者的是x64的)

	> [如何查詢你的 Windows 系統是 32 或 64 位元？ - 重灌達人](https://briian.com/7853/windows-32bits-64bits.html)

	要注意安裝的時候要把 `Add Ruby Executable to your PATH` 勾起來！

	![Ruby下載畫面](/images/2015/12/Ruby2.jpg)

	> 就算忘了勾，後續還是有辦法加進去的，這個晚點說。

2. 在[同一個頁面][Ruby官網下載]下載相對應的Ruby DevKit：  
	找 Other Useful Downloads 的地方下載與Ruby相對應的Ruby DevKit版本：

	![Ruby DevKit下載畫面](/images/2015/12/RubyDevKit1.jpg)

	並解壓縮到 `C:\RubyDevKit` ：

	![解壓縮Ruby DevKit](/images/2015/12/RubyDevKit2.jpg)

3. 使用 `Start Command Prompt with Ruby` (去程式集找Ruby的資料夾↓)

	![Start Cmd Prompt with Ruby](/images/2015/12/RubyDevKit3.jpg)

	**建立配置檔(configuration file)**

	1. 開啟`Start Command Prompt with Ruby`之後輸入

			cd c:\RubyDevKit  
			ruby dk.rb init

		> 配置檔是用來指向DevKit的文件。

	2. 編輯 `C:\RubyDevKit\config.yml` 這個配置檔

		加入 `- C:/Ruby21-x64` (或是你Ruby的安裝位置)

		![編輯Config](/images/2015/12/RubyDevKit4.jpg)

	**安裝DevKit**

	在 `Start Command Prompt with Ruby` 輸入：

		ruby dk.rb install

這樣就安裝好了！

[Ruby官網下載]: http://rubyinstaller.org/downloads/

#### 安裝Python & Pygments

`Pygments`是`Python`句法的標記。在Jekyll上的句法標記有pygments和`Rouge`，後者則是Ruby為基礎的標記。若是要以GitHub Page作為網站伺服，依據[Tod][]的說法，因為GitHub Page跑Jekyll時是用 `--safe` 模式，所以只能選擇pygments。但若以其他伺服器則可以選擇Rouge或其他的標示。這裡是以pygments為預設設定。

Python請至[官方下載頁面](https://www.python.org/downloads/)安裝**2.7.X**的版本(**不是**python 3.x喔，否則不能跑pygments)。另外安裝python的時候也要把加進PATH選起來：`Add Python.exe to PATH`。(如果沒選，方法一樣後面說。）Pygments的安裝則是在安裝python2之後`cmd`或`power shell`的地方輸入：

	python -m pip install Pygments

> 因為我有同時安裝python2與python3，所以我的指令是：  
> `py -2.7 -m pip install Pygments`  
> [官方解法：Python Launcher for Windows說明](http://gece.gitcafe.io/hexo/2015/06/22/在Windows下同时安装使用python2和python3/)

##### 意料外的差錯

後面在測試Jekyll的時候，我的Git shell一直跟我說我沒安裝......，最後是以gem install的方式安裝了pygments.rb才成功：

	gem install pygments -v 0.6.0

### 安裝Jekyll與安裝前的準備

我安裝的Jekyll與其他軟件的版本：

* Jekyll 版本：3.0.1
* wdm(Windows Directory Monitor) 版本：0.1.1

> 我因為安裝時沒有指定版本，安裝完才發現超新，但是最後確定能使用。
>
> * [On Windows][on Win]頁面確認過的最高版本是 v2.4.0  
> * [Tod][]的則是用 v2.5.3 (應該也是他當時安裝的最新，因為他沒特別提到版本問題)    
> * [官方說有問題](https://github.com/jekyll/jekyll/issues/1948)的是 v1.4.3

#### 安裝Jekyll前的確認(確認前面的東西都安裝的妥妥的)

用下面指令（可以使用Git Shell、Power Shell或cmd)：

	where.exe python
	where.exe ruby

兩個指令各會回傳執行檔的位置，如下圖：

![comfirm](/images/2015/12/prepare.jpg)

測試過若用cmd可直接以`where`代替`where.exe`

> `where.exe` 等同 `which`

確認都能找到就能進行下一步了。出現錯誤可能的原因是安裝python2跟ruby的時候沒有勾選加進PATH。

##### 將python2與ruby加入環境變數PATH

其實安裝的時候把那個勾起來都是把執行檔的路徑直接加入環境變數的PATH中，電腦就可以在找檔案的時候先查看PATH中的路徑。

左下角Windows > `電腦` 右鍵 > `內容`

![加入PATH](/images/2015/12/PATH1.jpg)

在左側點選`進階系統設定`

![加入PATH](/images/2015/12/PATH2.jpg)

點選`環境變數`

![加入PATH](/images/2015/12/PATH3.jpg)

在`系統變數`找`Path`，點選並`編輯`，加入以下兩個路徑：(或者是你python.exe與ruby.exe所在的資料夾路徑)

> C:\Python27;C:\Ruby21-x64\bin;

路徑間以`;`隔開。

確定完成後，需重新啟動才能修該環境變數。重開之後再以上面的指令確認，即可。

#### 安裝Jekyll！

1. 讓我們繼續使用Git Shell！接著輸入以下指令安裝Jekyll:

		gem install jekyll

	> 因為我沒有碰的SSL error，如果有碰到，可參考[Tod][]。

	Jekyll會安裝比較多東西，會跑一陣子。

2. 修改預設標記

到`C:\Ruby21-x64\lib\ruby\gems\2.1.0\gems\jekyll-2.5.3\lib\site_template` 編輯配置檔 `_config.yml`，在最後面加上預設標示：

	highlighter: pygments

![highlighter](/images/2015/12/InstallJekyll1.jpg)

#### 安裝wdm

Windows Directory Monitor可以幫助你看部落格post的改變，並自動重新編譯。  
參考下面兩個網站，我最後是安裝0.1.1版：

* [Add line of code to Gemfile that already contains that line of code - Stack Overflow][]
* [currently failing "gem install wdm" on a windows 8.1 x64 box #18][]

一樣在Git Shell輸入：

	gem install wdm

> 因為目前0.1.1是最新版的，所以就沒有指定版本直接安裝

不過我在安裝的過程跳了不知道是什麼的錯誤。

![install-wdm-err](/images/2015/12/wdm1.jpg)

最後也什麼都沒做，試個兩三次就安裝成功了。

[Add line of code to Gemfile that already contains that line of code - Stack Overflow]: http://stackoverflow.com/questions/32723710/add-line-of-code-to-gemfile-that-already-contains-that-line-of-code
[currently failing "gem install wdm" on a windows 8.1 x64 box #18]: https://github.com/Maher4Ever/wdm/issues/18

### 測試Jekyll

創一個測試用資料夾`c:\BlogTest`，並移動到前面這個路徑。

	cd c:\BlogTest

接著執行：

	jekyll new

Jekyll會自動幫你產生一個基本的網站，藉著再執行：

	jekyll build

接著想在本地預覽網站的話，可以用：

	jekyll serve

![localhost](/images/2015/12/Jserve.jpg)

接著就可以輸入上面那個網址預覽網站，顯示如下圖：

![localhost](/images/2015/12/Jserve2.jpg)

按`Ctrl+C`再按`Y`停止預覽。

> 你可以繼續用這個測試部落格(但若要用在GitHub Page需修改名稱)或刪掉。

### 以GitHb Page為伺服

執行：

	gem install bundler
	gem install github-pages

安裝Bundler: package bundle manager  
安裝GitHub Page的支援套件
另外依據[Tod][]還安裝了一個叫 `redcarpet` (a Ruby Markdown-parser) ，這是一個用在用在GitHub上渲染Markdown的格式文本。這就依個人需求安裝吧，不裝也可以。

GitHub Page有些指示教你怎麼建立Repository，就是作為網站的儲存庫

* [GitHub instruction](https://pages.github.com)

或是Fork別人儲存庫的方式：

* [BLOGGING ON GITHUB - PART 1 GETTING STARTED](http://digitaldrummerj.me//blogging-on-github-part-1-Getting-Started/)

這邊列幾個可以參考的：

* [Jekyll Bootstrap](http://jekyllbootstrap.com)
* [Lanyon A Jekyll theme](http://lanyon.getpoole.com/about/)

其中Jekyll Bootstrap的特色是讓Jekyll的新手可以快速上手，theme等也可以模組化套用，因為自己從0開始架站其實要建立的東西很多。我自己就是用JB，但是現在關於theme與其他架構的東西都還完全不懂......，所以也只能提供大家一點點資訊啦。

> 記得Fork下來的儲存庫中的`_config.yml`要改成自己的使用者名稱與網站網址喔！

另外要注意的是現在GitHub Page的預設網址是`http://USERNAME.github.io`。USERNAME是你GitHub的帳號。
> 舊的是用`http://USERNAME.github.com`，好像因為一些安全問題改掉了。

所以儲存庫的名稱就要使用 `USERNAME.github.io` 這樣的格式。

在網路上設定好儲存庫後，只要複製下來本地：

	 git clone git@github.com:USERNAME/USERNAME.github.io.git

做你想要的修改：

	git add .
	git commit -m "Your-Message"

再push上去：

	git push origin master

就能更新Blog啦！
> 雖然講得那麼簡單，但是稍微了解一下Git之後，發現還有很多需要學習呢。
> `git push` 如果有問題，可以參考這篇：[How can I push to my fork from a clone of the original repo?](http://stackoverflow.com/questions/25545613/how-can-i-push-to-my-fork-from-a-clone-of-the-original-repo)

#### 設定特殊網域

因為我還沒試過所以不清楚，大致好像就是加一個`CNAME`的檔：

* [Setting up a custom domain with GitHub Pages - GitHub Help](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/)
* [玩物尚誌][] 也有提到一點

### 最後，更新所有東西

* 更新部落格post(`_post`資料夾)
* 跑`gem update`
* ......

> 不過這是[Tod][]的文章最後的內容，我自己是不太敢更新啦，目前就是先能用，求穩定再說吧！

### 結語

我還有很多東西在學習，包含完全不知道JB的網站架構應該要怎麼修改成自己想要的...，多虧了[Tod][]的PO文讓我安裝Jekyll起來無壓力。中間還有碰到一些問題，也是搜了很多文章，這才發現英文真的很重要。就算只是略懂，但不能正確地理解語意也是徒勞。

那時候就想，也許也可以把自己的經驗分享(都有這個站了，不打文章可惜！)，也讓其他人可以比較不同文章，知道一下哪個版本是目前可行的。(感覺[on Win][]的版本更新很慢呀ry)

最後，希望大家會喜歡！一起來玩Jekyll，互相分享、指導與學習吧！
