---
title: "XAMPP安裝設定及簡單 PHP練習"
slug: "xampp-setup-1"
date: 2017-09-10T07:39:23+08:00
draft: false
tags:
- XAMPP
- Apache
- PHP
categories:
- Programming
#disqusIdentifier: fdsF34ff34
keywords:
- XAMPP
- Apache
- PHP
clearReading: true
#thumbnailImage: image-1.png
#thumbnailImagePosition: right
#autoThumbnailImage: yes
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

# 源起

之前提到的胡立大大在 Slack 群組裡發布了他擬的教學實驗計畫大綱，大概分為以下四段：  

1. 網頁後端相關（Session, Database, Server）  
2. 網頁前端相關（HTML, JavaScript, CSS, jQuery）  
3. 程式解題相關（帶大家做一些 ACM 一二星題或是基本演算法資料結構）  
4. 資訊安全相關（SQL Injection, CSRF, XSS）  

裡面還有一堆細項，總之就從頭開始練習，第一項就是「在自己的電腦上成功運行 PHP」，還有給提示可以用 XAMPP 架環境，然後用 PHP 寫 hello world，那就來試試看吧。

# 學習目標

學習用 XAMPP 建構環境，並用 PHP 寫一句 hello world。

# 學習內容

## 什麼是 XAMPP

[XAMPP官網](https://www.apachefriends.org/zh_tw/index.html) 的解釋是一個 PHP 開發環境，是一個 Apache 的發行版本，包含了 MariaDB、PHP 和 Perl。

完全看不懂，先來查一下名詞。

PHP 我大概知道，是一種後端的語言，理論上可以配合各種 SQL 語言跟資料庫作溝通，然後再跟前端連結作輸出。至於 PHP 到底算不算程式語言這種問題就跳過。

Apache 則是久聞其名但不知其詳。谷哥上的資料看起來是一種網頁伺服器，但伺服器是什麼？我沒念過計概，我也不知道計概教不教這個，總之就是沒概念，只好再查。

運氣很好，又找到這篇 [[WDC] 淺談 Web Server 及 Application Server （上）](http://blog.ericsk.org/archives/662)，終於有點概念，這邊說的 server 就是提供 web 服務的伺服器，而不是實體的機器。所以 Apache 就是提供 web 功能的伺服器程式。依照這個脈絡，所謂的 PHP 開發環境，應該是 XAMPP 提供可以運行 PHP 功能的 Apache 伺服器環境，也包括可以運行 MariaDB 跟 Perl。

這樣看來，XAMPP 應該就是類似一個打包的軟體，一次幫你安裝設定好可以運行 Apache、PHP、MariaDB 及 Perl 的伺服器環境，把個人電腦當伺服器跟資料庫來使用。

## 安裝 XAMPP

安裝的步驟，我是參考重灌狂人 [這篇](https://briian.com/18718/)，因為八月三十還有更新，而且順帶解釋了安裝步驟。
  
第一個碰到的重點就是防毒軟體。就 XAMPP 安裝程式的說明，因為防毒軟體的關係，為了怕有寫入上的問題，建議安裝路徑不要設定在 `C:\Program Files (x86)` 裡面，而是放在安裝程式預設的路徑 `C:\xampp` 就好。
  
第二個問題就是要安裝那些工具？server 端的 Apache 跟 MySQL 都必須要裝；FileZilla FTP Server 是可以讓別人透過 FTP 上傳或下載檔案，因為 XAMPP 是裝在我自己電腦上，所以這項我沒有安裝；Mercury Mail Server 是一個郵件伺服器的工具，因為猜想 PHP 的郵件功能可能要透過這個工具來運作，所以我點了安裝；Tomcat 則是 JSP 開發環境，JSP 是啥我都不知道，果斷放棄；至於程式語言，我自己是預計只練習 PHP，所以 Perl 我沒安裝；phpMyAdmin 是一種資料庫管理工具，好用，裝；Webalizer 則是 web server 記錄檔分析軟體，好像對後續網站流量分析有用，這我有裝，之後來研究怎麼分析；Fake Sendmail 好像也跟 PHP 發送郵件功能有關係，先裝。
  
然後安裝好就直接打開 XAMPP 的 Control Panel 控制台，記得起碼要把 Apache 跟 MySQL 打開，就是按 Start 打開。
  
這時候很可能碰到第三個問題，port 80 被佔用，所以 Apache 打不開。立刻求助谷哥大神，了解到問題其實就是有其他程式或服務佔用了這個 port，導致 Apache 無法正常運作。所以很自然地就有兩種解決辦法，一是關掉並停用佔用了 port 80 的程式或服務，二就是讓 Apache 換一個 port 用。
  
我個人是覺得因為很可能佔用的程式或服務我並不了解停用後會有什麼問題，而且要查是哪個程式或服務也有點麻煩，所以我傾向第二種做法。就很簡單，在 XAMPP 的 Control Panel 裡，Apache 的那一列按 Config，會跳出列表，選擇 httpd.conf 這項，就會打開一個記事本。找到 `Listen 80` 這行，改成 `Listen 8080`，然後存檔關閉記事本檔案，再次按下 Start，應該就可以運行 Apache 了。只是要注意一下，之後在瀏覽器開啟 XAMPP 的時候就不能只輸入 `http://localhost`，而是要輸入 `http://localhost:8080`。若能打開 Apache Friends 頁面，就表示 Apache 運作正常。
  
至此，XAMPP 就算是安裝設定完成了，接下來就寫個小 PHP 測試一下。

## 寫測試 PHP 網頁

接下來寫個小 PHP 網頁，就隨便打開任何一種文字編輯器，Sublime Text、Brackets、Notepad++ 都可以。PHP 語法就是要自己學習的部分，我是輸入下列：

```php
<?php echo "Hello World!"; ?>
```
  
接著存檔取名 `helloworld.php`，然後將檔案移到這個資料夾內 `C:\xampp\htdocs`。開啟瀏覽器，輸入 `http://localhost:8080/helloworld.php`，如果畫面有出現 Hello World! 字樣，就表示今天可以睡覺啦，謝謝大家~~~~