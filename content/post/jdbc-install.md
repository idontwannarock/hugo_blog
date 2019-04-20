---
title: "MacOS安裝JDBC-Eclipse"
date: 2017-11-23T14:48:17+08:00
draft: true
tags:
- MacOS
- JDBC
- Java
- Eclipse
categories:
- Programming
- Java
#disqusIdentifier: fdsF34ff34
keywords:
- MacOS
- JDBC
- Java
- Eclipse
clearReading: true
#thumbnailImage: image-1.png
thumbnailImagePosition: right
#autoThumbnailImage: yes
metaAlignment: center
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showMeta: true
---
<!-- toc -->
# 前言
為了貫徹在不同平台上都能同步工作進度的目標，要想辦法在MacOS上也能進行Java及JDBC開發。

# 安裝
在MacOS上要進行JDBC的開發，首先必須要安裝好資料庫，這邊以MySQL為主。

## 安裝MySQL
MacOS原本預設就有安裝好MySQL，所以不用特別安裝，只需要打開系統偏好設定，最底下的MySQL，然後Start MySQL Server，它左邊的字會變成綠色的running。

## 安裝資料庫管理程式
Mac上可以考慮MySQLWorkbench或Sequel Pro，免費版的功能算足夠，cask上都找得到，不知道怎麼用cask安裝的可以參考我的[這篇文章][0]。

## 載入MySQL JDBC connector


[0]: https://idontwannarock.github.io/hugo_blog/2017/11/%E6%88%91%E5%9C%A8macbook-pro%E7%9A%84%E8%A8%AD%E7%BD%AE---2017%E7%89%88/#軟體環境設置