---
title: "Java資料型態與轉換方式(1) - 基本型態"
date: 2018-02-09T10:00:29+08:00
draft: true
tags:
- Java
- convert
categories:
- Programming
- Java
#disqusIdentifier: fdsF34ff34
keywords:
- Java
- type conversion
clearReading: true
thumbnailImagePosition: right
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

紀錄自己在學習Java中歸納的各種資料型態轉換的方式，這篇先探討基本型態的轉換。

# 基本型態

## 基本型態簡介

Java裡規定了資料的八種基本型態`boolean`、`char`、`byte`、`short`、`int`、`long`、`float`、`double`。

其中`boolean`布林值是一種表示`true`真跟`false`偽的值，而不是數值，因此是唯一一種無法轉換成其他基本型態的資料。

而`char`則是字元，注意在 Java中，字元跟字串是不一樣的，這部分 Javascript就很不同，Javascript中沒有字元字串之分。

然後`byte`、`short`、`int`、`long`這四種就是整數型態，預設分別使用1、2、4、8個byte的空間來儲存其整數值。

最後`float`、`double`這兩種是浮點數

## 變數與常數

## 基本型態 -> 基本型態

除了`boolean`以外的其他七種型態之間有兩種轉換方式，一種是確認相容之後直接`=`轉換，另外一種則是用`(cast)`的方式轉換。

而基本型態之間的相容性首先要注意是變數還是常數