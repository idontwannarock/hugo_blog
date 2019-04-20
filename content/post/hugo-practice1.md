---
title: "練習用 Hugo架部落格在Github Pages(1)"
slug: "hugo-practice-1"
date: 2017-09-09T00:17:31+08:00
draft: false
tags:
- Hugo
- Github Pages
- Markdown
- SSG
categories:
- Programming
#disqusIdentifier: fdsF34ff34
keywords:
- hugo
- githubpages
- ssg
- markdown
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
# 源起
17年9月7日在 ptt Soft_Job版看到胡立大大 po文準備作一個計劃-建立 Slack群組來幫助大家練習討論一些網頁相關的東西，而我需要多作一些練習，並且最好能有人詢問或討論所以加入。  

而9月8日胡立大大就回信了，基本上就是解釋他想建立一個開放的群組，群組裡沒有老師，他擔任類似助教的腳色，會固定提出練習的題目，解答一些疑問跟提供一些資源這樣。  

其中胡立大大有提到希望大家能養成自學、解決問題以及歸納知識的習慣，我覺得很有道理很重要，所以剛好他也有提到希望大家學習「怎麼用靜態部落格產生系統」，可以練習怎麼使用靜態部落格產生系統、Git 的基本操作以及 Github 的相關知識。  

所以，就來吧！
# 學習目標
學習怎麼用靜態部落格產生系統 Hugo，並且把部落格架在 Github Pages上面。
# 學習內容

## 什麼是靜態、動態
就我看網路多種說法，歸納的概念大概是部落格或網站本身顯示不需要重複跟 server端交流的就算靜態，反之就算動態；最近因為 SEO的興起，還有一種偽靜態。  
## 什麼是靜態部落格（網頁）產生系統 Static Site Generator
在網路上找到[這篇文章](https://www.sitepoint.com/7-reasons-use-static-site-generator/)，講得蠻清楚的。  

在講什麼是靜態部落格（網頁）產生系統 Static Site Generator(SSG)之前，應該講一下內容管理系統 Content Management System(CMS)，例如 Wordpress。  

CMS的理念是讓作者不用擔心部落格，也就是網頁輸出的各種技術問題，只需要選擇喜歡的模板 template，就可以使用 CMS提供的文字編輯器寫作，節省很多技術上的麻煩，相信有用過 Wordpress都能理解。  

但相對之下 CMS就有一些壞處，例如只能使用 CMS提供的編輯功能（不然還是要會網頁或程式知識去作修改）、因為很多動態功能所以伺服器工作比較重可能影響效能、可能因為某些軟體或功能升級或資料庫出問題而導致網頁也出問題。  

而 SSG算是在 CMS跟完全自己 coding寫網頁架部落格的中間，比較知名的有 Jekyll跟 Hugo，或胡立提到的 Hexo。  

對 SSG我的認知是有點像在前端方面簡化的 CMS。還是有 template或 themes，但寫作部分一般用 Markdown語法寫作來簡化文字編輯功能，但也給予很大的自由度，因為有些近似自己寫 HTML，所以要修改什麼功能或加什麼 widget，都不用像 Wordpress要透過 plugin的方式加入，而是可以直接嵌入，但相對的其實也需要對 HTML語法有一些認識。  

而後端方面 SSG跟 CMS就很相似，通常兩者都有作後端一條龍的服務（要收費），也可以自己另外選擇伺服器跟資料庫儲存網頁內容。  

所以 SSG好處就跟 CMS相對，如自由度比較大、因為靜態網頁不需要一直跟伺服器交換資料而提高效能、因為原則上只使用基本 HTML+Markdown所以網頁出問題機會小。  

另外有一些其他好處，如因為幾乎沒有伺服器端的功能所以安全性高、因為類似在寫網頁而能作到版本控管（事實上 Wordpress也有這個功能，但只限於草稿的樣子）。  

當然 SSG最大的問題就是技術門檻明顯比 CMS要高得多，而且因為 Markdown語法本身的限制，文字排版美觀等功能比較受限制，只能靠技術跟美感自己去修正。
## 什麼是 Markdown語法
剛剛講到 Markdown語法，算是一種更簡化的 HTML語法。我是因為 Github的 README說明檔都用 Markdown寫而接觸過，但要注意 Markdown在 Github跟一般網頁的顯示會稍有不同。  

因為簡化過，所以非常簡單，可以參考[這個網頁](http://markdown.tw/)來學習。  

當然 Markdown語法的簡化導致它本身並不能作太多排版跟美化，但相對的好處就是一致性，這在寫筆記或說明的時候相當有用。  

另外，若習慣寫筆記歸類在 Evernote上，其實 Evernote也能讀 Markdown，只是沒辦法直接在 Evernote上編輯，方法需要自己找。我自己是用 Sublime Text的 plugin來編輯跟上傳 Markdown筆記到 Evernote上，這應該能給大家一個方向。
## 什麼是 Github
剛剛提到 Github，感覺這是目前寫程式必備，因為是基於版本管理工具 Git建立，算是跟其他工程師交流兼有履歷的功能吧，工作上不知道使用度如何。我有點把它當文件儲存空間，因為基本上沒有空間限制，只有針對單檔、Repository的大小限制。  

原本的版本管理工具 Git是一種幫助專案協作的工具，因為其版本管理功能強大而受到廣泛的使用。問題就是因為要一直用 command命令來使用功能，而且儲存的空間有時不方便遠距協作，於是 Github就誕生了。  

Github有點像網路共享空間，讓大家可以把 code都放在網路空間，並配合 Git的版本控制功能，採用圖形介面不用 command來使用功能，大大的方便了協作，並且促進了 open source的討論跟合作。但因為 Github本身文字編輯的功能並不強而且幾乎沒有測試運行的功能，所以多數人還是習慣在自己電腦本機上作業後上傳，而且上傳常常還是在本機電腦用各種 Git command來作基本版本管理並上傳，所以還不是非常方便。  

但是，最近幾年 Github推出 Github Desktop我個人認為幾乎彌補了這部分的缺陷。Github Desktop是 Github提供的桌面應用程式，可以協助管理本機版本並有圖形介面的上傳功能，讓你不用再記各種 Git command。只是不知道實務上使用度如何。
## 什麼是 Github Pages
Github有提供靜態網頁的 hosting功能，可以把網頁直接存在 Github的 Repository裡面，然後生成靜態的網頁。不過Github Pages有[一些限制](https://help.github.com/articles/what-is-github-pages/)要注意。  

對，其實 Github本身就有提供靜態網頁生成的功能，而且前面提到的 Jekyll根本是 Github親兒子，Github Pages直接推薦使用，也可以參考。
## 怎麼使用 Hugo架設網頁在 Github Pages
我選 Hugo是因為他用 Go語言寫的，感覺很潮，呵呵。不是啦，是因為 Hugo環境設定最簡單。  

因為全都要用 Git的功能所以全都要安裝 Git這個就不用比了。Jekyll是 Ruby on rails(ROR)寫的，使用前要安裝 ROR；胡立大大提到的 Hexo要裝 Node.js跟 nvm；只有 Hugo雖然是 Go寫的，但不用安裝 Go，只要把執行檔下載下來設定好環境變數 Path就可以使用。不用安裝一堆我最喜歡惹~  

在功能教學上，我個人覺得其實 Hugo官網並沒有寫得很好，不管中文還是英文都一樣，後來各種解法都是別人自己寫的心得，譬如我找到一個講的比較清楚的這篇：用[Hugo搭建個人網站](https://brent-li.github.io/post/build-personal-site-with-hugo/)，但我完全照作也是到後面 Git操作那邊就掛點，怎麼都傳不上去，搞到焦頭爛額。  

下一篇再來寫我完整的作法，我並不是本科出身，有很多基礎知識不清楚，只能從別人寫的作法中去理解，有問題請見諒，也可以提出來指正我，謝謝大家，今天就到這邊。  

這裡是[下一篇](https://idontwannarock.github.io/hugo_blog/2017/09/hugo-practice-2/)。