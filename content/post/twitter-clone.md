---
title: "4th Practice: Twitter Clone"
date: 2017-09-15T10:27:28+08:00
draft: false
tags:
- PHP
- MySQL
- MVC
- Bootstrap
categories:
- Programming
- 100 Practice
#disqusIdentifier: fdsF34ff34
#keywords:
#- github pages
#- hugo
clearReading: true
thumbnailImagePosition: right
metaAlignment: center
coverImage: "http://res.cloudinary.com/dcvgho2zc/image/upload/v1505442582/4th-practice-cover-1024x535_p6n4e1.png"
coverCaption: "As ugly as it can be"
coverMeta: out
coverSize: full
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showMeta: true
---
<!-- toc -->

# 第四個目標

練習 PHP, MySQL 跟 MVC，因為 Bootstrap 很方便所以 HTML 跟 CSS 就這樣吧廠廠~

作品：[史上最簡陋Twitter](https://goo.gl/PVUtXQ)  
參考：這參考太多了，只能說各種參考orz  
原始碼：可以參考[我的Github](https://github.com/idontwannarock)  

還是要先講一下，這並不是我憑空寫出來的作品，是跟著 Udemy 網路課程教學作出來的。

# 遇到困難

## 對自己智商產生質疑

真的是這樣，之所以這麼廢的東西還能作這麼久，事後檢討的結果，絕大多數時間都浪費在因為智商太低產生的各種製造障礙，簡稱製障問題上。

譬如說出現什麼 404 或 500 錯誤訊息，花了三個多小時觀看 stackoverflow 上高手討論，最後發現是 PHP 某一行少加了一個 `;`，當天直接氣到作不下去之類的…

## debug

作這個真心受教了，要馬每一步都先作測試，要馬就要會查 bug，人生就是要接受 bug 的出現，沒 bug 絕對是陰德值爆滿。

所以我目前領悟到的順序是：

> 1. 先查 code 有沒有漏加什麼 `;` 或 `,`或者哪裡括號沒關好，這些出現的頻率超乎你想像，即使有 autocomplete 功能也是一樣
> 2. 再來用 Chrome 的 `Inspect` 或 Firefox 的 `Inspector` 來查錯誤訊息，運氣好就會跟你說你程式碼哪一行有問題
> 3. 還找不到，先不要急著 google，先查 Log！先查 Log！先查 Log！很重要，所以講三次。通常 Log 也會跟你講執行到哪一行有問題
> 4. 最後真的都不行，再拿錯誤訊息去拜 google 大神

以上是我的切身之痛，其他的難點在這兩個困難底下，都已經不再重要…喔不是啦，還是補充一個。

## AJAX

不太確定這算不算常識，但大家在使用 jQuery+AJAX 的時候要注意 jQuery 的版本，請不要用到 slim 版的喔， jQuery slim 版把 AJAX 功能拿掉了，所以最起碼要用 minified 或更完整的版本，切記切記！

尤其在套 Bootstrap 4 的模板的時候要注意，官方預設是載入 slim 版本的 jQuery，要記得自己去改 cdn。