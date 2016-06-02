---
layout: post
title: "利用 Docker 在 Windows 執行 Jekyll (1)"
description: ""
category: Jekyll
tags: [Jekyll, Docker]
---

#### 開頭

!!
因為換了電腦，一直沒有重新架環境。最近心血來潮，忽然又好想重新弄好這個站。搜尋後恰巧又翻到 [James Sturtevant][Running-with-Docker] 的部落格，使用 [Docker][docker] ...... 。為了省去安裝一堆套件的麻煩、避免不同環境各種相容性的問題，決定騰出時間在新電腦上試試。

**使用系統: Windows 10 x64**

[Running-with-Docker]: http://www.jamessturtevant.com/posts/Running-Jekyll-in-Windows-using-Docker/
[docker]: https://www.docker.com

### 使用 Image for GitHub pages

> 使用的Image為: [Starefossen/docker-github-pages][Starefossen]

> 教學參考: [James Sturtevant][Running-with-Docker]

1. [安裝 Docker toolbox](https://docs.docker.com/windows/)
2. 使用 `Docker Quickstart Terminal` (開啟後，請等待初始化)
3. 移到 **repository (repo)** 內 (存放 `_config.yml` 的位置)，若沒有任何 repo，可以去 fork 一個或 fork [Jekyll Bootstrap](https://github.com/plusjade/jekyll-bootstrap)
4. 輸入下列指令
  > $ docker run -v "$PWD":/usr/src/app -p "4000:4000" starefossen/github-pages

  若電腦裡沒有 `starefossen/github-pages` 這個 Image，則需等待一段下載時間。

  之後只要在瀏覽器輸入 `<DOCKER_MACHINE_IP>:4000`，就可以在電腦本地端測試網站`git push`上去之後的樣子。

  若不知道 Docker machine IP 是多少可以在 `Docker Quickstart Terminal` 使用指令：

  > $ docker-machine env default

  通常會是 `192.168.99.100:4000`。

#### 雜項

按照指示利用 `ctrl + c ` 停止之後，無法再使用相同指令。可用指令 `docker ps` 查看運轉中的 container，再以 `docker stop <contrainer-ID>` 停止該 container。

![allocated-problem](/images/2016/05/allocated.PNG)

> 應該還有更好的方法 (也許 `docker restart` ?)，我目前對 Docker 不太熟，就不誤人子弟了。

#### Troubleshooting

* **權限**

  在 [James Sturtevant][Running-with-Docker] 的文章裡 #Project location for Docker on Windows 這段有提到執行後，因為權限問題無法正常運作的情形 ([issues #91][iss91])。網路上找到一篇 [Docker on Windows綁定主機目錄到容器內卷的問題][颜俊标] 提到，因為權限限制，只能和 `C:/Users` 以下的位置作為與VM之間的共享目錄。

  解決方法有:
  1. 將 repo 移到 `C:/Users` 之下
  2. 可參考 [Docker on Windows綁定主機目錄到容器內卷的問題][颜俊标] (我沒試過，sorry)

[Starefossen]: https://github.com/Starefossen/docker-github-pages
[iss91]:https://github.com/jekyll/docker/issues/91
[颜俊标]: http://yanjunbiao.me/2016/01/03/Volume-Mount-Issue-of-Docker-on-Windows/


#### 結語
一陣子沒碰，GitHub Pages也完全把 Jekyll 升到 3 以上了，以至於現在的站還有一堆問題要解決。有了想要重頭了解Jekyll (目前僅 fork Jekyll Bootstrap 湊合著用) 的念頭。下一篇會記錄用 Jekyll 官方的 docker image。
