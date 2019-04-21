---
title: "3rd Practice: Click Click Ben"
date: 2017-09-15T10:11:46+08:00
draft: false
tags:
- JavaScript
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
coverImage: "http://res.cloudinary.com/dcvgho2zc/image/upload/v1505442040/3rd-practice-cover_zigtzi.jpg"
coverCaption: "What a beautiful Ben"
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
# 第三個目標

練習 JavaScript 跟 `random()` 函數。  

作品：[Click Click Ben](https://goo.gl/sgAjR3)  
參考：大帥哥 [Ben Hsieh](https://www.facebook.com/ben.shieh.3) ~

# 遇到困難

## 帥哥阿 Ben 照片太難挑

這是我製作這個作品中碰到最大的困難！太多太帥了，我無法選擇！！我的媽！！！誰來救救我！！！！

## 照片亂數出現位置及亂數間隔時間

其實這個問題我之前就有學過，所以這邊大概紀錄一下作法。

先用 JavaScript 的 `Math.random()` 來亂數產生 0-1 的浮點數，然後為了適應各種大小的視窗，要乘上 `document.documentElement.clientHeight` 或 `document.documentElement.clientWidth` 來亂數產生要往右或往下多少 px 的數字。

然後用 `document.getElementById("id").style.top` 或 `document.getElementById("id").style.left` 來設定位置。

亂數間隔時間則用 `setTimeout()` 來作，記得括號的兩個參數要用逗點分隔，第一個參數是暫停後要執行的程式，第二個是暫停的時間，單位是千分之一秒。

## 控制照片出現或消失

原本想都用 JavaScript 控制，但發現直接寫好所有 HTML+CSS 後，用 `display: block;` 跟 `display: none;` 來控制最方便。

## 控制次數

這也沒什麼好說的，只是做個記錄。

最基礎的做法就是設一個變數，然後用 `if` 判斷來控制次數。

控制次數感覺可以用 `for` 或 `while` loop 來寫，但中間要卡一個按的功能，不知道能不能行？