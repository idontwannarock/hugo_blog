---
title: "練習用 Hugo 架部落格在 Github Pages(2)"
slug: "hugo-practice-2"
date: 2017-09-09T15:22:03+08:00
draft: false
tags:
- Hugo
- Git
- Git Bash
- Github Pages
- SSH
categories:
- Programming
#disqusIdentifier: fdsF34ff34
keywords:
- githubpages
- git
- ssh
- gitbash
clearReading: true
#thumbnailImagePosition: right
metaAlignment: center
#coverImage: image-2.png
#coverCaption: "A beautiful sunrise"
#coverMeta: out
#coverSize: full
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showMeta: true
---
<!-- toc -->

> 這篇文章是初學的時候撰寫的，其中一些觀念並不正確，步驟也可能因為更新或觀念問題而不適用或者多餘，此篇文章僅為留做紀錄

# 學習目標

學習怎麼使用 Hugo 架設網頁在 Github Pages。

# 學習內容

## 環境設定

我並非本科，所以以下作法全都是從各官網跟谷哥研究而來。先說明我只會用 Windows，而且是 Win10，所以想用 MacOS 或 Linux 的可以左轉出去自己上官網跟谷哥研究。

環境設定這邊需要作幾件事，設定 Hugo，設定 Git，新增 Github 帳號，跟設定 SSH，除了設定 SSH 要最後作以外，其他順序無所謂。

## Hugo 環境設定

如同上一篇所述，Hugo 雖然是 Go 語言寫的，但現在的版本並不用安裝 Go，只要到 [這個網址](https://github.com/gohugoio/hugo/releases) 下載最新版本，找地方解壓縮，然後將解壓縮後的 exe 檔路徑設定到 Path 環境變數裡面就可以了。

比較完整的流程應該是先創建 Hugo 目錄，例如 `C:\Hugo`，然後建兩個子資料夾 `bin` 和 `Sites`。下載 Hugo 最新版本的 zip 檔，解壓縮到 `bin` 資料夾裡面，若 exe 檔檔名不是 `hugo.exe` 就改成 `hugo.exe`。

然後要設定 Path 環境變數，厲害的人可以直接用 cmd 設定，就不講了。來講我這種菜鳥的方法，右鍵點開始鍵（就是狀態列 Windows 圖案的那個鈕），選「系統」，然後選右上方的「系統資訊」，跳出來視窗後，選左邊的「進階系統設定」，再跳出一個視窗後，選「進階」頁面下方的「環境變數(N)...」，會再跳出一個視窗分成上下兩區塊，在上方的使用者變數區塊，變數那一欄找到 Path 後，連點兩下又會跳出一個新視窗，這次直接按右邊的「新增(N)」，然後填上剛剛 `hugo.exe` 的路徑，例如 `C:\Hugo\bin`，最後再一路按確定以及關閉視窗出去。

然後為了確定是否有設定成功，請再右鍵點一次開始鍵，選「Windows PowerShell(系統管理員)(A)」來打開 PowerShell，然後直接輸入 `hugo version` 後按 Enter 鍵，如果有顯示出版本資訊，那就是設定成功。

## 安裝 Git、申請 Github 帳號及設定 SSH

這段建議直接參考另外一篇筆記來操作。

[Git及 Github基礎認識](https://idontwannarock.github.io/Hugo-Blog/2017/09/git-and-github-basic-1/)

## 生成基本網頁

這邊會用到一個簡單的指令，跟一些 Hugo 本身的指令。主要會用到移到資料夾位置的 `cd` 指令，所以不太會的人可以谷哥了解一下。

請先打開前面建立好的 `C:\Hugo\Sites` 資料夾，對資料夾內空白處點右鍵，選擇 Git Bash Here 開啟 Git Bash，這樣就預設好路徑是在 `Sites` 資料夾內。

接著輸入以下指令生成基本的網頁。

```
hugo new site Hugo-Blog
```

這樣就會在 `Sites` 資料夾內生成 `Hugo-Blog` 資料夾，並有以下目錄結構：

```
|--archetypes 
   |--default.md # 生成文章的模板  
|--content       # md 檔案存放位置  
|--data  
|--layouts  
|--static        # 圖片等存放位置  
|--themes        # 模板主題目錄  
config.toml      # 網站配置屬性
```

`config.toml` 是紀錄網站配置屬性的文件；`content` 則是放網頁的內容，之後寫的 md 檔會放在這邊；`static` 資料夾則存放圖片等東西。

## 生成新文章

網頁的內容 md 檔建議在同樣的 Git Bash 用以下命令生成，因為用命令生成的 md 檔會有內建的 `front matter`，記錄三項必備資訊，`title`、`date（生成時間）`及`draft（草稿狀態）`。裡面比較重要的是 `draft`，預設是 `true`，意思是還是草稿，網頁上並不會顯示出來；若完成後想發布到網頁上顯示出來，請記得將此項改為 `false`。

```bash
cd Hugo-Blog  # 切換到 Hugo-Blog 資料夾路徑  
hugo new post/firstPost.md
```

如此，Hugo 就會自動在 `content` 資料夾中建立 `post` 資料夾，並在其中建立 `firstPost.md` 這個 md 檔案。

剛剛有提到，裡面生成的 `front matter` 包含了一些資訊，然後就可以在 `front matter` 區塊底下開始用 [Markdown語法](http://markdown.tw/)寫 blog 了。

## 設定 theme

接下來可以選擇喜歡的網站主題，可以到這邊選擇 [Hugo themes](https://themes.gohugo.io/)。

這邊有個問題我還沒找到解法，就是這些 theme 幾乎都提供 `git clone` 的方式下載，ssh 連線方式沒問題，但我不知道為什麼用 https 連線的方式從來沒有成功過。不知道有沒有人知道可能的原因？

接下來以我選擇的 [casper主題](https://themes.gohugo.io/casper/) 來示範 ssh 連線的作法。

首先進入 [casper主題](https://themes.gohugo.io/casper/) 點選 Download 進入其 Github 資料夾，點右邊綠色 Clone or download 按鈕，點藍色 Use SSH 連結切換到 Clone with SSH，再複製 url。

接著同樣用剛才打開的 Git Bash 輸入以下指令：

```bash
mkdir themes
cd themes
git clone git@github.com:vjeantet/hugo-theme-casper.git casper
```

這幾行指令就是先在 `Hugo-Blog` 資料夾內建立 `themes` 資料夾，然後移動路徑到 `themes` 資料夾內，再下載 casper 主題到 `themes` 資料夾。

接著針對 `Hugo-Blog` 資料夾內的 `config.toml` 檔案作一些修改。
    
```
baseURL = "https://idontwannarock.github.io/Hugo-Blog"  
languageCode = "zh-TW"  
title = "Wang's Blog"  
paginate = 5  
DisqusShortname = "Wang Cheng Hao"  
Copyright = "&copy; All rights reserved - 2017"  
canonifyurls = false  
  
[params]  
description = "Ignorance is a bliss..."  
cover = "images/cover.jpg"  
author = "Wang Cheng Hao"  
authorlocation = "Taipei, Taiwan"  
authorwebsite = "https://idontwannarock.github.io/Hugo-Blog"  
authorbio= "邁向軟體工程師"  
logo = "images/logo.jpg"  
#googleAnalyticsUserID = ""  
#Optional RSS-Link, if not provided it defaults to the standard index.xml  
#RSSLink = "http://feeds.feedburner.com/..."  
githubName = "idontwannarock"  
twitterName = "CH_Howard_Wang"  
facebookName = "howard.wang.3990"  
linkedinName = "cheng-hao-wang-a2298289"  
#set true if you are not proud of using Hugo (true will hide the footer note "Proudly published with HUGO.....")  
hideHUGOSupport = false  
 
[[menu.main]]  
name = "Blog"  
weight = 200  
identifier = "blog"  
url = "/"  

[[menu.main]]  
name = "About me"  
weight = 190  
identifier = "about"  
url = "/about"
```

其中比較重要的就是 `baseURL`，`https://使用者名稱.github.io` 是 Github Pages 固定生成的網址，後面則是接你預計要儲存資料的 Repository 的名稱。

然後 `canonifyurls` 要記得設置為 `false`，否則生成的網頁會抓不到主題配置。

當然我也會相應的將選好的 `cover.jpg` 以及 `logo.jpg` 兩張圖片放到 `static\images` 資料夾當中。

其他資訊都可以自己修改或參考 [casper主題](https://themes.gohugo.io/casper/)的說明。

## 生成測試網頁

接著建議用 Hugo 自帶的 server 功能作一下測試，在剛才打開的 Git Bash 中輸入以下命令：

```bash
cd .. # 切換到上一層 Hugo-Blog 資料夾路徑  
hugo server -t casper
```

若成功，在瀏覽器網址列輸入 `http://localhost:1313/Hugo-Blog/` 來預覽，有哪裡不喜歡或不舒服就直接修改 md 文件或 `config.toml`；有錯誤就依照 Git Bash 指示的問題去改。

## 生成網頁

若測試沒問題，就可以執行以下命令來正式生成網頁：  

```
hugo -t casper
```

這時 Hugo 會用選定的 casper theme 來生成網頁，並放在自動建立的 `public` 資料夾當中。

## 上傳到 Github

接著再上傳整個 `public` 資料夾到 Github 上之前，請先用瀏覽器到 Github 上面建立一個 Repository，假設叫做 Hugo-Blog。建立好之後，請點中間 SSH 那個按鈕，後面會生成 SSH 的 url 網址，把那個網址複製下來；若建立 Repo 的時候有勾 README 選項，則按右邊綠色 Clone or download 按鈕，點藍色 Use SSH連 結切換到 Clone with SSH，再複製 url。

接著在剛才的 Git Bash 輸入以下命令：

```bash
cd public # 切換到 public 資料夾路徑
git init # 生成 Git 紀錄
git add . # 將 public 資料夾內全部檔案 staging
git commit -m "Initial commit." # commit 所有已 staging 的檔案  
git remote add origin git@github.com:idontwannarock/Hugo-Blog.git # 加入遠端資訊
git push -u origin master # 將本地的 master branch push 到 Github 上的 origin/master branch
```

其中 `git remote` 那行後面的網址請貼上你在 Github 複製的 SSH url。

等 Git Bash 顯示上傳完成後，上 Github 的 Hugo-Blog Repository 檢查資料都上傳好之後，就可以到 `config.toml` 這個檔案裡面 `baseURL` 所記錄的網址去看新生成的網頁；這個網址也可以到 Github 對應的 Repo 裡面，Settings 底下的 Github Pages 區塊找到。

這邊是一些基本的 Git 功能，將 `public` 資料夾內的東西上傳到 Github 已經建立好的 Hugo-Blog 這個名稱的 Repo，Github Pages 就會抓取其中 `index.html` 檔案來生成靜態網頁。

後續如果新寫了一些 md 檔存在 `content\post` 資料夾中想要上傳到網頁上，只需要進到 `public` 資料夾右鍵打開 Git Bash，執行以下命令：

```bash
git pull origin master # 先把 Github 的主版本抓下來以免衝突
cd .. # 切換到 Hugo-Blog 資料夾路徑
hugo server -t casper # 一樣先測試網頁看有沒有需要修改
hugo -t casper # 生成網頁
cd public # 切換到 public 資料夾路徑
git add .
git commit -m "說明文字"
git push origin master
```

即可更新變動。

如果覺得這些 Git 指令太麻煩，其實可以用 Github Desktop 來完成上傳的操作，非常方便。

大 guy 4 醬。

如果對 Git 指令不熟悉，可以參考我另外寫的 [這篇筆記](https://idontwannarock.github.io/Hugo-Blog/2017/09/git-and-github-basic-1/)。