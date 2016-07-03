---
layout: post
title: "將已存在的 local 儲存庫上載到 GitHub"
category: Git
tags: [Git, GitHub]
---

### 前情

大概是因為使用舊版的 `JB` 架構，反正也想重頭摸 Jekyll，所以想把之前的 posts 移到新的儲存庫裡。把之前用 `Jekyll/docker` 產生基本 jekyll 架構的資料作為新站的儲存庫。

### 把已存在的資料夾變成 Git 儲存庫

開啟 `Git Bash` `cd` 到資料夾位置後，使用：

```
$ git init
```
會產生一個隱藏的 `.git` 資料夾，裡面會自動產生一個 repo 必要的 metadata。

接著要先來個 `first commit`！

```
$ git add .
$ git commit -m "Our first commit!"
```

### 在 GitHub 上建立一個**未初始化的空白Git儲存庫**

紅色框框的地方不要勾選就行啦！

![create-empty-repo](/images/2016/06/create-empty-repo.PNG)

複製此儲存庫的 URL (後面.git那串) 先備著。

### 將本地端儲存庫的 remote 設定成 GitHub 上的儲存庫

```
$ git remote add origin [GitHub上儲存庫的URL]
```
![add-remote](/images/2016/06/add-remote.png)

用下面的指令可以確認 remote 的設定：

```
$ git remote -v
```

![verify-remote](/images/2016/06/verify-remote.png)

接著將本地的改變推到GitHub上，就 OK 啦：

```
$ git push origin master
```
> 這裡，
>
> origin 代表 [remote name]；
>
> master 代表你要推的 [branch name]。

若以後只想使用 `git push`，就要先設定其 `upstream` 為哪個 branch：

```
$ git push --set-upstream origin master
```

這個指令不只設定，也有 push 新的東西上去。

或者可以用，`Git branch` 設定 upstream：

```
$ git branch -u origin/master
Or
$ git branch --set-upstream-to origin/master
```

### 參考資料
* [官方文件：Adding an existing project to GitHub using the command line](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/)
* [Setting up a repository](https://www.atlassian.com/git/tutorials/setting-up-a-repository)
