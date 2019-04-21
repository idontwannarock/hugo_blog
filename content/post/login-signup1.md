---
title: "實作簡單登入會員系統(1)"
slug: "login-signup-function"
date: 2017-09-11T07:11:59+08:00
draft: false
tags:
- PHP
- MySQL
- Login
- Signup
- Logout
- myslqi_real_escape_string
- hash
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

# 學習目標

1. 實作簡單會員系統，有加入會員、登入、登出
2. cookie
3. 防範 SQL Injection+XSS
4. hash 密碼

# 學習內容

## 構思

坦白說，我有自學過一點點前後端的 Udemy 網路課程，所以前端的部分，簡單的 HTML, CSS, Javascript, jQuery 我還可以，大概是不會寫也可以谷哥看別人怎麼寫的程度。後端也是學過簡單的 PHP 跟 MySQL 這樣。所以後面的說明很可能會省略很多基礎，而只記錄我不太會或不太熟的部分。

關於會員系統，Udemy 課程的老師其實有教過這個部分，但當時似懂非懂，幾乎就是 copy 老師的程式碼，糊里糊塗就寫出來，PHP 跟 MySQL 的部分一片模糊，所以先來嘗試自己重新寫一遍，不行再來找找看網路教學。

要寫登入登出的功能，我第一個想到就是要用 HTML 的 `form` 先做三個 `input` 跟一個 `button`，若要串接資料庫，應該還要再作一個 `button` 切換 Sign Up 跟 Login 畫面來作區別。預計應該要用 jQuery 控制切換 Sign Up/Login 的功能。

然後後端邏輯應該就是先作 Sign Up/Login 資料的驗證部分，用 `ajax` 傳輸資料到後端，檢查輸入的 `username`、`email` 跟 `password` 是否空白、格式是否正確以及是否重複，用 `echo` 輸出錯誤提示訊息給前端。

接著作 Sign Up 部分，接著剛剛驗證完資料正確後，檢查資料庫有無重複資料後，再把 `username`、`email` 跟 `password` 存進資料庫。

最後再作 Login 部分，先用使用者輸入的 `username` 比對資料庫有無紀錄，再比對 `password`，最後輸出 Login 成功訊息。這邊會感覺會需要了解 `$_SESSION` 跟 `$_COOKIE` 怎麼運作，因為要幫 Sign Up/Login 成功的使用者加上 `$_SESSION` 或 `$_COOKIE`。

接著作 SQL Injection 及 XSS 攻擊的防範。最後再將使用者 Sign Up 時輸入的 `password` 作 hash 處理。

另外以下是以只架站在自己 Windows 電腦的 XAMPP 上為前提，XAMPP 架站簡單教學可以看我之前寫的這篇筆記：[XAMPP安裝設定及簡單 PHP練習](https://idontwannarock.github.io/hugo_blog/2017/09/xampp-setup-1/)。

還有就是如果想要讓自己寫完的作品可以讓別人看到，可能要自己先想辦法查做法，我自己都還搞不太清楚。（攤手）

## 版面設定

所以就從寫個 `form`、三個 `input` 跟兩個按鈕開始好了。我猶豫了一下要不要用 Bootstrap，還是用好了，畢竟練習的重點在後端，畫面就直接套用現成的版就好。

所以直接就貼上 Bootstrap 4 的 [Starter template](https://v4-alpha.getbootstrap.com/getting-started/introduction/#starter-template)，因為後面要用 `ajax`，所以 jQeury 的版本記得從 slim 換成最起碼 min 的版本。然後直接用 Bootstrap 的 [Forms](https://v4-alpha.getbootstrap.com/components/forms/#form-controls) 作模板。

## 切換功能

接下來就是複習 jQuery 語法的時候，因為這邊用到的功能不難所以不多講。大概方向就是在 `click` 動作上建立一個判斷式，判斷目前是 Login 轉 Sign Up 要做什麼事；Sign Up 轉 Login 要做什麼事。這部分的 `script` 我是寫在 `body` 的最後。

切換畫面有個小技巧記錄一下，作一個隱藏的 `input`，然後設定 `value="1"`，這樣在用 jQuery 判斷的時候用這個值作判斷條件會比較簡單。不然只是純粹要切換畫面修改 CSS，應該用 `.toggleClass()` 就可以了。

前端的部分大概就這樣，接下來開始練習後端部分。

## 設置資料庫

先去 XAMPP 的 Control Panel 把 MySQL 打開，然後去瀏覽器輸入 `http://localhost:8080` 來進去 Apache Friend 頁面，點選右上角的 phpMyAdmin 進入資料庫管理的頁面。直接左邊點選 New 來建立一個新的資料庫，我設定資料庫名字為 `user`，新 table 名稱 `userData`，四欄分別是 `id`、`username`、`email` 跟 `password`，並設定 `id` 欄位為 Primary Key 以及 Auto Increment。

設定 Primary Key 的目的是確保此欄位的每一筆資料都是獨一無二的；Auto Increment 則是讓資料庫自動遞增設定 `id`。

## 連接資料庫

接下來就要用 PHP 的 mysqli 函數庫語法嘗試連接資料庫，我是用以下方法，並用 PHP 的 `print_r` 來顯示連結問題。

```php
$link = mysqli_connect("localhost:3306", "root", "", "user");  
if(mysqli_connect_errno()) {  
    print_r(mysqli_connect_error());  
    exit();  
}
```

記錄一下 [`mysqli_connect`](http://php.net/manual/en/function.mysqli-connect.php) 的語法是 `(host, username, password, dbname)`。這邊因為是本機，所以 `host` 就是 `localhost:3306`，3306 是 XAMPP 預設給 MySQL 的 port，如果你有調整，這邊就要相應的更改；本機上的 `username` 就是 `root`，不確定可以到 phpMyAdmin 的首頁看；`password` 預設應該就是沒有，如果有設定（我還真不知道怎麼設定）這邊就要改；最後 `dbname` 是剛剛設定的 `user`。

`mysqli` 是 PHP 的 MySQL 函數庫增強版，功能更強，安全性更好；所以之前的 `mysql` 已經漸漸淘汰不用。

接著則是用 `mysqli_connect_errno()` 來判斷連接是否有錯誤，若有錯誤則用 `print_r` 來顯示 `mysqli_connect_error()` 的錯誤訊息。

[`mysqli_connect_errno()`](http://php.net/manual/en/mysqli.connect-errno.php) 是回傳最近一次連接的錯誤「代碼」；[`mysqli_connect_error()`](http://php.net/manual/en/mysqli.connect-error.php) 則是回傳最近一次連接的錯誤「訊息」。

最後則用 `exit()` 來停止繼續執行 script（官方文件側面證明 PHP 是 script？XD）。括號裡面可以填上停止執行同時要顯示的訊息，若裡面填上 integer（0-254 之間），則會被用來當錯誤代碼而且不會顯示出來。功能跟 `die()` 是一樣的。

## 設計結構

再來先講一下設計的檔案結構。

因為我在 Udemy 上的課最後的作業是把常用的 function 單獨存成一個 `function.php` 的檔案，然後把會跟 `index.php` 直接互動的部分放在 `action.php` 並且在開頭就 `include("function.php");` 這樣來操作。

據說這叫 MVC 啦，我也不是很懂，但覺得這樣分開蠻清楚的，就這樣作吧~

## ajax 傳資料

接著要寫 `ajax` 傳資料的功能。

在前面切換 Login/Signup 按鈕的後面，我是先寫這樣來測試 `ajax` 功能是否正常傳送我要傳送的資料：

```jquery
$.ajax({  
    type: "POST",  
    url: "action.php?action=loginSignup",  
    data: 
        "username=" + $("#username").val()
        + "&email=" + $("#email").val()
        + "&password=" + $("#password").val()
        + "&loginActive=" + $("#loginActive").val(),  
    success: function() {  
        alert("username=" + $("#username").val()
        + "&email=" + $("#email").val()
        + "&password=" + $("#password").val()
        + "&loginActive=" + $("#loginActive").val());  
    }  
})
```

這邊其實是設定用 `POST` 傳送 `data` 內的訊息，但也同時用 `GET` 的方式傳送一個 `action=loginSignup` 的訊息來說明要作 Login/Signup 的動作，讓後端執行 `action.php` 的時候，知道要做哪個動作，我在 `action.php` 內也會相應的寫上判斷 `$_GET['action'] == "loginSignup"` 的條件。這算是為未來可以把這個功能套用到別的地方使用的功能標記方法。

順便記錄一下 `GET` 跟 `POST` 的差別。`GET` 會把要傳送到 server 的資訊以明碼的方式放在 URL 網址後面，長度有限制；`POST` 則是將資料放在 http request 裡面，是隱藏的，相對沒有長度限制。這兩種都是 http 協定中定義的跟伺服器互動的方式。我覺得這篇講得蠻簡單明白：[Go Web 程式設計入門教學：Web 基礎](http://happycoder.org/2017/07/02/golang101-tutorial-web-basic/)

如果按了 Submit 按鈕有跳出 `alert` 顯示 `data` 的內容，就表示作對了。

## Login 驗證功能

這時候先到 `index.php` 表格上方增加一個隱藏的 `div`，`id` 設為 `loginAlert`。

接著到 `ajax` 的 `success` 改成以下：

```javascript
success: function(result) {  
    if (result) {
        $("#loginAlert").html(result).show();
    }  
}
```

用意是先把所有 `action.php` 回傳的東西，傳到 `id` 為 `loginAlert` 的這個 `div` 並顯示出來。

接著到 `action.php` 用各種判斷式判斷 `username`、`email` 跟 `password` 是否空白或符合格式，若不符合，就儲存一段顯示錯誤的話進另外設定的變數 `$error`，到最後判斷 `$error` 是否空白，若否則 `echo $error;` 並 `exit();`，也就是把 `$error` 裡面的錯誤訊息傳回 `ajax` 之後，停止繼續執行 `action.php`。

這邊需要一些判斷式觀念，記錄一下基礎：

1. `if` 是判斷 `()` 內的條件是否為真後，執行 `{}` 內的內容。
2. `if...else` 是判斷 `()` 內的條件是否為真後，執行 `if` 接著的 `{}` 內容；不為真則執行 `else` 接著的 `{}` 內容。
3. `if...else if` 是先判斷 `if` 後 `()` 的條件，為真則執行接著的 `{}` 內容；不為真，則再開始判斷 `else if` 接著的 `()` 內條件，為真則執行接著的 `{}` 內容。最後還可以再接 `else`，作用為當 `if` 跟 `else if` 判斷式 **皆** 不為真的時候，執行接著的 `{}` 內容，此為 optional。
4. 需要多條件判斷有兩種方案，一是在 `if` 判斷式中用 `and`、`or` 這種聯立條件的方式，但這種是 **同時** 判斷多條件；若需要 **依序** 判斷多條件，則採用 `if...else if` 的方式。

但想像是美好的，現實是骨感的，一執行立刻就碰到問題：alert 區塊一閃而逝，好像畫面重新刷新，所以 alert 區塊又重新回到隱藏的狀態。這邊很顯然是 Submit 按鈕的問題，剛好作個筆記，要記得把 Submit 按鈕的 `type` 改成 `button`，若是維持原來的 `submit`，每次按下去就會刷新畫面，`ajax` 帶動的效果就都跑掉了。

對了，還要記得去 XAMPP Control Panel 把 MySQL 也打開，不然也會悲劇 XD

## PHP 語法跟函數庫

接著要先學習一些 PHP 跟 SQL 的寫法，語法可以到 [w3schools](https://www.w3schools.com/default.asp) 或 [PHP 官網](http://php.net/manual/en/index.php) 查詢。先記錄幾個用到的：

* [SQL](https://www.w3schools.com/sql/default.asp)
    1. [`SELECT 範圍 FROM table 名稱 WHERE 判斷式`](https://www.w3schools.com/sql/sql_where.asp)：這個功能是按照`判斷式`回傳指定 table 裡面的資料。`範圍`就是要選取的欄位，全選就填上 `*`。
    2. [`INSERT INTO table名稱 (`欄位一`, `欄位二`, ...) VALUES ('欄位一資料', '欄位二資料', ...)`](https://www.w3schools.com/sql/sql_insert.asp)：在指定 table 裡面增加資料。
    3. [`UPDATE table名稱 SET 範圍 WHERE 判斷式`](https://www.w3schools.com/sql/sql_update.asp)：依照`判斷式`更新指定 table 裡面指定欄位的指定資料。
    4. `LIMIT`：是 MySQL 特有的子句，通常接在 `SELECT` 句子的最後面，用來限制回傳的資料筆數。功能類似 `TOP` 跟 `ROWNUM`。
* PHP 各種 [預設變數](http://php.net/manual/en/reserved.variables.php)、[變數控制函數](http://php.net/manual/en/ref.var.php)、[`mysqli` 函式庫](http://php.net/manual/en/book.mysqli.php)
    1. [`mysqli_query($link, $query)`](http://php.net/manual/en/mysqli.query.php)：對資料庫執行一次動作。`$link` 通常是要事先用 `mysqli_connect` 設定好連結的資料庫；`$query` 通常代表用 SQL 指令設定好要執行的動作。
    2. [`mysqli_num_rows`](http://php.net/manual/en/mysqli-result.num-rows.php)：讓資料庫回傳查詢到的資料筆數。
    3. [`mysqli_fetch_assoc($result)`](http://php.net/manual/en/mysqli-result.fetch-assoc.php)：獲取某指定資料同列（同 Primary Key）的所有資料，`$result` 代表要參照的資料。
    4. [`mysqli_insert_id($link)`](http://php.net/manual/en/mysqli.insert-id.php)：取得前一次對資料庫執行動作（通常是 `INSERT`）而自動產生的 `id`，`id` 欄位須具備 Auto Increment 屬性。

我其實沒有正規的拿一本 PHP 或 SQL 的書來念，基本上都是上前面提到的 [w3schools](https://www.w3schools.com/default.asp) 跟 [PHP 官網](http://php.net/manual/en/index.php) 這兩個網站查各種功能怎麼用，所以也許觀念不見得非常正確。

另外有關於 mysqli 函數庫的部分，他支援兩種表達方法：object-oriented 跟 procedural。我這邊都是用 procedural。

## Sign Up 功能

再來準備寫 Sign Up 加入會員的功能，這邊就要牽扯到把會員資料記錄進資料庫的部分。記得要把這些功能寫在 `action.php` 的 `echo $error; exit();`這個部分的後面，否則會變成前面判斷輸入資料有問題還繼續執行寫入資料的問題。

首先要加入會員，都要先判斷剛填好的 `username` 跟 `email` 是否有跟資料庫內的重複。我是用 `mysqli_num_rows` 來作判斷式，大於 0 就表示有資料這樣。然後用 `INSERT INTO` 來新增資料到資料庫。

## Login 功能 -> cookie | session

然後登入會員是用 `mysqli_fetch_assoc()` 來抓比對到的 `username` 同組資料，再跟 `POST` 裡的 `password` 比對。

接下來就是要研究 session 跟 cookie 的差別以及用法。我查到這篇 [[簡明] COOKIE 與 SESSION 的基本原理](http://blog.webgolds.com/view/353) 寫得蠻清楚的。

我最後選擇用 cookie，因為感覺比較像是目前普遍的做法，加入會員後不用每次進入網站都要重新登入，但設定每次登入只維持登入狀態一個月。

這裡同樣列出用到的 PHP 語法：

1. [`setcookie('變數名稱', '變數值', '保存時間')`](https://www.w3schools.com/php/php_cookies.asp)：建立 cookie，保存時間是以秒為單位；如果要強制消滅 cookie，就把保存時間設定為負數
2. `time()`：目前時間。這裡是用來結合 `setcookie` 的保存時間使用

我的作法是結合前面的判斷式，在判斷出可以加入會員以及可以登入那邊加上 `setcookie`，並原則上設定 30 天 (`time()+60*60*24*30`，並 `echo "1";`) 來回傳一個 `1` 跟 `ajax` 表達目前是已經登入的狀態。

然後回到 `index.php` 的 `ajax` 那邊，將原來長這樣的：

```javascript
success: function(result) {  
    if (result) {
        $("#loginAlert").html(result).show();
    }  
}
```

改成這樣：

```javascript
success: function(result) {  
    if (result) {
        window.location.assign("http://localhost:8080/login-signup/");
    } else {
        $("#loginAlert").html(result).show();
    }  
}
```

這裡的 [`location.assign`](https://www.w3schools.com/jsref/met_loc_assign.asp) 是讓首頁重跑一遍，回到原始狀態，但已經建立好的 cookie 不會消失，所以還是登入的狀態。所以後面的網址要填上最初始首頁的完整網址。這樣做可以把 GET 放在網址列後面的資訊消除。

## 登入狀態表示

接著要回到 `index.php` 的表格那邊作一些調整。讓 client 端在載入網頁的時候先判斷有無 cookie 存在，若有就顯示 "You have successfully logged in!"，若無則顯示原本的表格。若你有另外作 Logout 按鈕，作法類似。

我這邊還有參考 w3schools 用 [Javascript 設定跟尋找 cookie 的方法](https://www.w3schools.com/js/js_cookies.asp)。

作出來的作品可以參考這裡：

- [作品網站 Sign Up Login Function](http://idontwannarock-com.stackstaging.com/project/login-signup/)
- [我放在 Github 的原始碼](https://github.com/idontwannarock/Tiny-Projects-and-Functions/tree/master/login-signup)  

當然，為了放在託管 server 跟資料庫給大家直接試驗網頁，實際路徑跟資料庫等等會跟上面敘述的有差別。

## SQL Injection 及 XSS 簡單防範

我在網路上參考了這兩個網站來理解 SQL Injection 跟 XSS。

- [你知道什麼是「SQL Injection」(SQL 攻擊)嗎？](https://pcrookie.com/?p=1950)
- [甚麼是 XSS？簡介黑客常用攻擊技倆](https://www.hkitblog.com/?p=23318)

就我的粗淺的了解，SQL Injection 跟 XSS 都是 client 端的攻擊手法，最常見的攻擊方法都是透過一個網頁中的輸入欄位（在我們這個作品當中就是各個 `input` 位置），來植入一些惡意的代碼，讓後來的瀏覽者或使用者碰到一些惡意的狀況、資料被偷取、被植入木馬等等。

而同樣就我理解到的簡單防範方法，就是先處理 `input` 傳過來的資料，轉換到我們需要的資料型態，來避免一些特殊符號如 `>/<^&$#@` 等等。

我這邊用到的是 PHP mysqli 函式庫的 `mysqli_real_escape_string($link, $data)`，要注意的是這個函式必須填上代表連線到資料庫的 `$link`，`$data` 則是要轉換成字串 (string) 的資料。`mysqli_real_escape_string` 這個函式會將定義的特殊符號作轉換來避免一些 SQL Injection 跟 XSS 的狀況。我是將所有會要跟資料庫作互動的 `$_POST` 都作處理。

請注意這個並不是一個完善的防範方法，只是作一個簡單的防範。

## 儲存密碼 - hash 及 salting

基本上如同胡立大大所說：「一個正常的網站是不會知道使用者的密碼是什麼的。」

就我的理解，一般來說如同這樣的會員功能，網站在接收到使用者傳輸的密碼的同時，就會進行密碼加密。

而早期通常會以 hash 的方式，例如 `md5` 加密，然後就存進系統。基本上就是把密碼通過 md5 設定的某種轉換模式，轉成一長串字串，一個字串只會對應一個密碼，而這種加密方式很難反向破解；所以最簡單的破解手法是建立常見的密碼 - 字串轉換表來對應，所以才會常常看到各種網站在加入會員的時候讓大家設定字母與數字混雜，而且不能是常用的密碼，來避免被駭客找到對應的字串作破解。

但這種方式比較大的問題是使用者常常記不得自己設定的密碼，所以後來又產生一種 salting 的作法，也就是在 hash 以前，在密碼的前面或後面加入一些基於特定規則或亂數產生的字串，用來增加密碼長度，或利用亂數來增加破解難度。

我是採取 [`password_hash`](http://php.net/manual/en/function.password-hash.php) 的作法，這個 PHP 的函數本身就有包括 salting，所以直接寫這樣來 hash：

```php
password_hash($_POST['password'], PASSWORD_DEFAULT)
```

但有件事要記得，用 [`password_hash`](http://php.net/manual/en/function.password-hash.php) 函數來 hash 的話，Login 時就要用 [`password_verify`](http://php.net/manual/en/function.password-verify.php) 函數來作判斷式來比對 `password`。艾租以~

# 感想

恭喜我作完這個簡單的功能，結果就是用網路查了一堆功能跟說明，倒是沒有直接搜尋 PHP 登入怎麼做，不知道這樣算不算自己作？XD

就先這樣吧，之後再來加上忘記密碼重設的部分~

再次附上作品網站跟 Github 原始碼網址：

- [作品網站 Sign Up Login Function](http://idontwannarock-com.stackstaging.com/project/login-signup/)
- [我放在 Github 的原始碼](https://github.com/idontwannarock/Tiny-Projects-and-Functions/tree/master/login-signup)

我又重構了一遍，嘗試增加以及改進一些部分。實作筆記在這：[實作簡單登入會員系統(2)](https://idontwannarock.github.io/hugo_blog/2017/09/login-signup-function-2/)