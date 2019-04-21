---
title: "Java 樂透抽取算法初探"
date: 2017-11-15T14:26:17+08:00
draft: false
tags:
- Lottery
- Algorithm
- Java
categories:
- Programming
- Algorithm
#disqusIdentifier: fdsF34ff34
keywords:
- Lottery
- Algorithm
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

因為做到這個經典練習演算法的題目，雖然是非常入門級的，也是讓我想了很久，覺得都做了這麼久，不記錄下來也是蠻可惜。

# 題目

請隨機從正整數 1-42當中隨機抽出 6個數字，不用排序，但不可重複。

# 解法

樂透這個題目主要可以練習的有三個地方，隨機、迴圈，還有就是如何確保數字不重複。

> 以 Java 來說，隨機就是使用 `java.lang.Math` 類別裡的靜態方法 `random()`，但要注意`Math.random()` 之後產生的是大於等於 0、小於 1，也就是 `0 <= Math.random() < 1` 的 `double` 型態浮點常數。  
> 因此，以這題來說，還要記得利用 `(int)` 轉換型態成整數型態的常數。  
> 另外，若不放心浮點數轉換為整數後的值，可以利用一樣是 `Math` 類別裡的靜態方法 `floor()` 或 `ceiling()` 來取無條件進位或無條件捨去後的整數值。
> 而產生指定範圍內的亂數的公式為 `Math.random() * 範圍個數 + 初值`

然後因為已經確定要抽出的數目，所以可以使用元素個數不能變動的陣列，當然也可以用可以變動個數的 `Collection` 或其子介面去解決。關鍵就在於不可重複。

這篇只討論陣列的解法。

## 暴力解：重複檢查

最簡單的寫法肯定就是暴力解：每抽出一個數字就存到結果陣列，然後每抽一次，就跟陣列裡每個數字都比對一次，一有重複就重抽。

```java
// 設定存儲樂透數字陣列
int[] randomArray = new int[6];

// 執行抽取樂透數字的動作 6次
for (int i = 0; i < randomArray.length; i++) {
    // 先將亂數出來的數字存入陣列第 i個位置
     randomArray[i] = (int)(Math.random() * 42) + 1;
    // 接著執行檢查迴圈
    for (int j = 0; j < i; j++) {
        // 輪流跟陣列中目前存在的其他元素比對
        if (randomArray[i] == randomArray[j]) {
            // 如果有找到重複數字，就將計數器 i減 1，然後重抽
            i--;
            // 注意這邊 break是跳出 if外面一層的 for迴圈
            break;
        }
    }
}

// 印出樂透數字陣列中的數字，列印陣列也要用迴圈，這邊是用新版寫法
for (int num : randomArray) {
    System.out.print(num + " ");
}
```

## Fisher-Yates shuffle

能解決問題的方法就是好方法，但暴力解有一個問題，因為要檢查已存入陣列的其他元素，所以抽到越後面就要檢查越多次，現在只有 42 個數字抽 6 個，萬一是從一百億中抽一百萬個不重複數字，那該檢查多久？

所以就有一個經典的演算法來解決這個問題，是兩位統計學家 Ronald Fisher 爵士以及 Frank Yates 於 1938 年提出的。

原始的演算法是為了解決一個問題：如何產生一串無重複數字的亂數數列。

這個算法其實已經經過很多改良，它的概念是這樣：

1. 先產生一串固定個數且照數值大小排列的字串
2. 然後隨機從數列中抽出一個數字
3. 將這個數字從原始數列中刪除
4. 將這個數字寫道另外一個數列的頭或尾
5. 重複步驟 2-4 直到所有數字都從原始數列刪除，並且都依照寫到另外一個數列中後停止

這個算法的目的就很好地確保了每次隨機抽取數字肯定不會重複，因為之前的數字都已經從要抽取數字的數列中刪除了。

而且因為不用每次都檢查，所以可以大幅提升效率。

我們利用這個算法不會抽取到重複數字的特性，可以延伸出解法如下：

```java
// 設定要抽取個數
int picks = 6;
// 設定樂透數字範圍起始數字及結束數字
int startNumber = 1, endNumber = 42;
// 設定儲存數字的陣列
int[] randomArray = new int[endNumber - startNumber + 1];
// 產生按照數值大小排序好的數列
for (int i = startNumber; i <= endNumber; i++) {
    randomArray[i] = i;
}

// 開始亂數程序，但我們不用將整個數列都亂數shuffle，只需要做我們要抽取個數，也就是 6次
for (int j = 0; j < picks; j++) {
    // 先設定一個暫存亂數數字的變數 randomIndex，這是要用來當指標指向陣列元素用的
    int randomIndex = (int)(Math.random() * (endNumber - startNumber + 1)) + 1;
    // 然後再設定一個暫存數字的變數 temp，暫存陣列中指標 randomIndex對應的數字
    int temp = randomArray[randomIndex];
    // 將 randomArray[randomIndex]跟第 j個元素對調位置
    randomArray[randomIndex] = randomArray[j];
    randomArray[j] = temp;
}

// 印出樂透數字陣列中的數字
for (int k = 0; k < picks; k++) {
    System.out.print(num + " ");
}
```

我有特別設定要樂透的數字個數，以及抽取範圍的起始及終止值，以便將來更動這三個參數就可以做各種不同範圍個數的樂透，甚至也可以利用 `java.util.Scanner` 的功能讓使用者能直接用鍵盤輸入這三個參數，不過那就不在這個題目要討論的重點。

# 限制

其實這些解法最大的問題都不在於算法本身，而是 Java 提供的 `random()` 方法是不是真正的隨機，其實這也可以寫一個程式來檢驗，我們將這個程式跑個幾千、幾萬，甚至幾百萬次之後，每一個數字抽到的次數是不是趨於相等。

就我現在粗淺的理解，基本上還沒有能產生真正隨機數字的演算法；或者說，能用演算法產生的隨機數字都不是真正的隨機，只是趨近於隨機。

畢竟只要提到演算，就代表有一定規則，而透過一定規則產生出來的東西就無法稱為真正的隨機。

而 Java 提供的 `random()` 方法則是透過線性同餘公式產生的偽隨機數，詳細可以參考 [維基][0]。

[0]: https://zh.wikipedia.org/wiki/%E7%B7%9A%E6%80%A7%E5%90%8C%E9%A4%98%E6%96%B9%E6%B3%95