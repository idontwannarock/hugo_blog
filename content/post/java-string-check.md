---
title: "Java字串判定(1) - 空字串 vs null"
date: 2018-02-06T14:09:25+08:00
draft: false
tags:
- String
- Java
categories:
- Programming
- Java
#disqusIdentifier: fdsF34ff34
keywords:
- String
- Java
clearReading: true
#thumbnailImage: image-1.png
thumbnailImagePosition: right
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

# 前言

因為開始做專題，開始要作資料檢查，首先會要碰到的就是最基本的檢查是否有輸入資料，也就是要檢查字串，記錄一下Java當中有關字串檢查的東西。

## 去除字串空白

這主要分兩個部分，一是去掉頭尾空白，一是去掉字串中間空白。

去掉頭尾空白就用`.trim()`，去掉字串中間空白則可以用`.replaceAll(" ", "")`的方式簡單完成。

但用`replaceAll()`方法有個小小的問題，就是萬一碰到的是空白字元，例如`\t`、`\r`這種就會有困難，所以必須要用正規表示式來去除，例如：

```java
String str = "\t";
str.replaceAll("\\s+", "");
```

## 檢查空值

接著如果要檢查字串是否有東西，要分成檢查兩種狀態，null或空字串。

這邊有幾個方法檢查這個部分，但要注意它們實際功能上的區別。

### `.length == 0`

這個是Java最原始的功能，基本上就是檢查字串長度是否為0，回傳值型態為boolean。

### `.isEmpty()`

這個方法是Java 6.0之後推出用來取代`.length() == 0`的方法。`isEmpty()`其實也是在檢查字串長度是否為0，回傳值型態一樣為boolean。

### `.equals("")`

這個功能是用字串的比對功能，比對是否為空字串，結果應該會跟前兩個方法相同。

### `!= null`

前面幾個方法都有一個共同的問題：萬一字串為null，全都來不及檢查就會跳NullPointerException。

所以必須要用這個方式檢查是否為Null，再檢查是否為空字串，也就是要寫成類似下面這樣：

```java
String string;
if (string != null && string.isEmpty()) {
    // things to do when string is neither null nor blank;
}
```

### `"".equals(string)`

但有一個更簡短的方法`"".equals(string)`。

因為用String本身的`.equals()`方法，會先檢查括號內參數字串是否為null，若是null就會直接回傳`false`；若參數字串不為null，才會繼續檢查是否跟`""`空字串相等。

所以前一段的檢查式就可以縮短如下：

```java
String string;
if (!"".equals(string)) {
    // things to do when string is neither null nor blank;
}
```

# 結語

雖然最後一個方法最簡短，但其實可讀性不見得比較優秀；而倒數第二個方法雖然比較囉唆，但整體上可讀性比較好。

所以要用哪種方法還是要看簡潔跟可讀性怎麼取捨。