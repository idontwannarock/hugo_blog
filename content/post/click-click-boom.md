---
title: "1st Practice: Click Click Boom"
date: 2017-09-15T07:36:23+08:00
draft: false
tags:
- HTML
- CSS
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
coverImage: "http://res.cloudinary.com/dcvgho2zc/image/upload/v1505435536/1st-practice-cover-1024x550_mdnblw.jpg"
coverCaption: "A beautiful click"
coverMeta: out
coverSize: full
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showMeta: true
showActions: true
---
<!-- toc -->
# 第一個目標

寫個簡單作品來練習 HTML 跟 CSS  

作品：Click Click Boom  
[黑白版本](https://goo.gl/vPtbzB)  
[粉紅大理石版本](https://goo.gl/CfT2Ro)  
[黑色大理石版本](https://goo.gl/NVdhAk)  

# 遇到困難

## 置中

左右置中很容易，但上下置中就麻煩了，還要隨瀏覽器視窗大小變動就更麻煩。

最後在 stackoverflow 查到一種解法，就是先設定 `position: absolute;`，然後 `top`、`bottom`、`left`、`right` 都設 `0`，再用 `margin: 0;` 來自動對齊。

## 套框

因為想要使用 HTML+CSS 作套框而不是用畫去背圖的方式，這真的殺死很多腦筋，內部框跟文字怎麼排都無法置中，對，又是無法上下置中，用 `text-align` 只能左右置中，`vertical-align` 完全不理我。

最後又是 stackoverflow 查到解法，要用 CSS3 的新 property，`display: flex;` 來解，然後設定 `align-item: center;` 跟 `justify-content: center;` 來上下左右置中，但當然衍伸出下個問題。

## 相容

瀏覽器太多種，新舊版本對 HTML5 或 CSS3 相容度又不一致，真的會搞死，實務上難道也是只能靠經驗？或出問題再來修改嗎？還是有更合理的作法？

最後是上 [w3schools](https://www.w3schools.com/) 一項一項 property 查相容再加相容敘述 `-webkit-` 或 `-moz-` 來解決。

## iOS相容

這個真的超哭，我整個都做完了，就只有在 iOS 裝置上，按鈕按不下去！

我先是想說應該是 `transform` 可能不相容，所以一樣查了 w3schools 加上相容敘述，結果還是不行！

以我的智商真的想不出來惹，最後只能跟阿混求救，大神就是大神，瞬間幫我找出答案，因為 `Pseudo class active` 跟 iOS 不相容……

當然阿混很好心的幫我查好解法，結果是要用 JavaScript 來解，這跟我只想練習 HTML+CSS 本意不符，但找了一下好像真的沒有更好的解法，所以最後還是用了這個解法。

# 感想

工程師真的很辛苦，但也很爽。能親手做出成品很有成就感！後續再來想要加什麼功能會更舒壓 XD