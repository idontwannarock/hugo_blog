---
title: "實作簡單登入會員系統(2)"
slug: "login-signup-function-2"
date: 2017-09-19T00:23:29+08:00
draft: true
tags:
- PHP
- MySQL
- Login
- Signup
- Logout
- Delete Account
- Ajax
categories:
- Programming
#disqusIdentifier: fdsF34ff34
keywords:
- php
- mysql
- login
- signup
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

前一篇筆記可以參考這裡：[實作簡單登入會員系統(1)][1]

# 學習目標

1. 加入 Bootstrap 的 Modal 功能
2. 全部改用 POST 傳遞資料
3. session 與 cookie 並用以因應更多功能及未來擴充

# 學習內容

## 緣起

因為前作有一些問題不確定怎麼解決，各種嘗試修改改到自己混亂，乾脆重作，並順便把一些功能加上去或留出空間擴充。

## 構思

這次試圖把常用功能，例如按下 Submit 按鈕都要檢查一次表格有無空白或有沒有填正確這種，分離到 `function.php` 裡面；如果可能再嘗試用 Javascript 來控制輸出畫面。

另外要加上 Login 後的歡迎畫面以及刪除帳號的功能。

## 前端設定

這部分就不多講了，就只是加上 Bootstrap 的 Modal 功能。只要記得，要觸發展開 Modal 的按鈕的 `data-target` 要設定為 Modal 最外層 `div` 的 `id`，然後按鈕的 `type` 一定要設定為 `button` 而不是 `submit`。

## Ajax 語法

記錄一下我使用到的這種 Ajax 語法。

```jquery
$.ajax({
    type: "POST",
    url: "action.php",
    data: {
        loginsignupstatus: $("#loginSignupStatus").val(),
        username: $("#username").val(),
        email: $("#email").val(),
        password: $("#password").val()
    },
    success: function(result) {
        alert(result);
    }
});
```

這邊 `type` 其實用 `method` 代替也可以，只是 `method` 會有老舊 jQuery 不適用的問題。`url` 就是要交換資料的目標網址。data 這邊用的是 Plain Object 描述，跟前一次 String 的方式描述不太一樣，但感覺這樣代碼比較易讀。`success` 這邊是先作測試回傳的值，要搭配 `action.php` 裡面用 `print_r` 或 `echo` 傳回來各種值，再 `alert` 出來，可以每段步驟檢驗是否有成功。

## 資料庫連線

[上一篇筆記][1] 教過設定資料庫，這邊更擴展一下，讓之後多資料庫的時候，擴充更方便。

這次我是建立一個 `connection.php`，用以下代碼：

```php
$link = mysqli_connect("localhost:3306", "root", "");
mysqli_select_db($link, $dbName);
if (mysqli_connect_errno()) {
    print_r(mysqli_connect_error());
    exit();
}
```

也就是讓要連到的資料庫 `$dbName` 可以隨我們需要再指定，這樣可以配合在需要處理有關資料庫的功能時，指定 `$dbName`，再 `include("connection.php)` 的方式連線資料庫。

這種有需要再連線資料庫的方式，就我理解通常是用在有大量要求連線資料庫動作的程式，為了避免一個人開一次連線裡面要做很多動作，但可能因此拖延到很多時間才結束，結果其他人的連線要求就會一直延遲到前面的人全都作完，而不能達到盡量即時的反應，因而降低使用者體驗降。

## call class function

受到胡立大大 slack 討論群組各位前輩的啟發，認真來研究把每個需要重複執行的功能獨立出去到 `function.php`，用 `class` 歸類再個別設定 `function`，要用的時候再 call 出來，相當方便，但就是要注意變數的設定是在哪個範圍，以及個別功能執行完要怎麼傳值出來作判斷或處理而不會全都傳回去給 `ajax`。

總之 `function.php` 內大概是這樣設定 `function`：

```php
class className1 {
    function functionName1() {
        //write function here
    }
    function functionName2() {
        //write function here
    }
}
class className2 {
    function functionName3() {
        //write function here
    }
    function functionName4() {
        //write function here
    }
}
```

我在 `action.php` 內呼叫的方法：

```php
include("function.php");
$callFuntions = new className1();
$callVar = $callFuntions->functionName1();
```

這樣可以分類會重複用到的功能，也可以需要的時候隨時呼叫需要的功能出來執行。新學一招，但最好每一個步驟都 `echo` 或 `alert` 個什麼東西確保沒有作錯。

從 class function 的角度想，其實也不用另外建立 `connection.php` 這個檔案，建立資料庫連結完全可以當成另外一個 `class function`，就這樣幹！

結果問題很大，最大的問題就是出在變數的 scope，如果把 `connection.php` 的建立資料庫指令改成 class 裡的 function 給別的 function 呼叫，最後都因為變數 scope 的關係無法在別的 function 裡面使用。這裡學到一招，用 `var_dump()` 配合 `echo` 的方法來檢查變數狀況。所以最後還是回到 `include("connection.php)` 的方式。囧>

## session 及 cookie

這次除了 cookie 以外，也加入 session。cookie 是給使用者未來再回到網頁時檢查登入狀況，session 則是處理使用者登入後在線上活動用。

[1]: https://idontwannarock.github.io/hugo_blog/2017/09/login-signup-function/