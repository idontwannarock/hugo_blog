---
title: "Markdown語法"
slug: "markdown-syntax"
date: 2017-10-22T15:42:04+08:00
draft: false
tags:
- Markdown
- HTML
categories:
- Programming
#disqusIdentifier: fdsF34ff34
keywords:
- Markdown
- HTML
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
# Markdown特色
## 1. 易編寫
相對於 HTML需要注意各種 tag、屬性、特殊字元，Markdown是更容易編寫的方式，雖然無法像 HTML那樣可以直接透過各種屬性，甚至 CSS來達到各種效果，但純粹以書寫來說，Markdown的功能已經相當夠用。
## 2. 轉換 HTML
不過如果有需要的話，Markdown可以用各種方式轉換成 HTML，以方便我們發布成網頁或部落格文章，網路上有相當多的程式可以達到這點；相對之下，從 HTML轉換回 Markdown就沒這麼方便了，主要原因就是 HTML有相當多屬性等並不被 Markdown支援，所以有轉換回 Markdown的困難。

但還是有補救的辦法，在編寫 Markdown文件的時候，其實還是可以使用 HTML語法的，我使用過的轉換器都可以讀取 HTML語法，並正常顯示以及轉換，所以真的有什麼 Markdown找不到的 HTML功能，就直接寫 HTML吧！當然這就需要對 HTML語法有更多認識了。
## 3. 編寫／視覺
 跟 HTML一樣，在編寫 Markdown的時候呈現的畫面，跟實際呈現的畫面其實是不一樣的。
 例如我們編寫 Markdown如下：
 
	- ***This*** is a [sample](http://example.com/ "example.com").

實際呈現的畫面其實是這樣的：

> - ***This*** is a [sample](http://example.com/ "example.com").

所以在編寫 Markdown的時候，最好找個可以隨時觀看實際畫面的編輯器來確認實際畫面。
# 區塊元素
## 換行
原則上按 Enter鍵就是換行。

要注意的是有些轉換器會要求不同的換行字元，例如有些會要求在行尾加上兩個空白，再按 Enter鍵，才代表換行；也有些會要求兩個空白加一個 tab鍵等等，所以建議要找可以即時顯示畫面的編輯器，隨時確認實際畫面。
## 分段
Markdown是以空白行來分段，原則上就是該行只有一個 Enter就換行。

同樣的，要注意有些編輯器會要求不同的特殊字元來代表空白行。
## 標題
Markdown支援 Setext以及 atx兩種形式的標題。一般都用 atx語法，標題的階層較多，語法也比較好記。
### Setex形式
以底線的方式來表示標題，只有兩種如下：

	This is an H1
	=============
	This is an H2
	-------------

實際顯示就會變成這樣：

> This is an H1
> ============
> This is an H2
> -------------

### atx形式
在標題前面加上 1到 6個`#`，剛好對應到 HTML的`h1`到`h6`，如：

	# This is an H1
	## This is an H2
	### This is an H3

實際呈現：

> # This is an H1
> ## This is an H2
> ### This is an H3

若你寫完有考慮轉為 HTML發布為網頁或部落格，確切使用標題是個好習慣。一是轉換完不用再花心思調整，只需要考慮 CSS或 Javascript做美化就好；二是良好的標題設定跟 SEO優化有關。
## 清單
與 HTML相同，也分為有序清單及無序清單。

### 有序清單
使用一個數字，加一個英文句點`.`，再空一格。

注意**數字並不會影響實際畫面的排序**，例如：

	9527. First item
    9487. Second item

實際上 Markdown會自動排序：

> 9527. First item
> 9487. Second item

但建議還是照正常順序編排啦，自己編寫看得比較清楚，而且也不清楚什麼時候 Markdown就改成一定要照順序排序（攤手）。
### 無序清單
使用`*`、`+`或`-`做無序清單的標記。例如：

	* First item
	* Second item
	* Third item

會顯示成：

> * First item
> * Second item
> * Third item

### 巢狀清單
不論是有序還是無序清單，都可以使用縮排 tab鍵來做出巢狀的清單。例如：

	* First item
		* Second item
			* Third item

會顯示成：

> * First item
>	* Second item
>		* Third item

## 區塊引言
使用`>`來標記區塊引言。例如：

	> This is a blockquote paragraph.

就會顯示成：

> This is a blockquote paragraph.

區塊引言也可以巢狀分層，例如：

	> This is a blockquote sentence 1.
    
	> > This is a blockquote sentence 2.

會顯示成：

> This is a blockquote sentence 1.

> > This is a blockquote sentence 2.

區塊引言也可以只在一個「段落」的第一行加入`>`標記區塊，記得「段落」是要以「空白行」做為區隔。

另外區塊內也支援 Markdown語法。例如：

	> *This* is a blockquote paragraph 1 sentence 1.
	**This** is a blockquote paragraph 1 ***sentence 2***.
	This is a blockquote paragraph 1 sentence 3.
    
	> > - [ ] This is a blockquote paragraph 2 sentence 1.

會顯示成：

> *This* is a blockquote paragraph 1 sentence 1.  
**This** is a blockquote paragraph 1 ***sentence 2***.   
This is a blockquote paragraph 1 sentence 3.

> > - [ ] This is a blockquote paragraph 2 sentence 2.

但注意區塊引言內常常會自動加上斜體屬性，所以強調的三種狀態在區塊引言內其實只會剩粗體一種。

## 程式碼區塊
在程式碼區塊內，Markdown語法並不會被轉換，所以可以如實呈現實際寫的 Markdown語法內容。若是其他種程式語言的程式碼，則會有限度的辨識，並標記出有支援的語法，這部分目前有很多擴充，容後再敘。

當然以 Markdown語法要做程式碼區塊，有幾種辦法，一是用<code>```</code>將整段程式碼包起來，一是在開頭用縮排 tab鍵來做標記，直到沒有縮排的一行空白行為止。

例如：

	```
	This is a code block.
	```

呈現起來會是這樣：

> ```
This is a code block.
```


## 分隔線
在同一行用三個以上的`*`、`-`或`_`可以組成一個分隔線，同一行不可以有其他的文字或標記，但在三個`*`、`-`或`_`中間可以插入空白。

以下幾種方式都可以組成分隔線：

	- - -  
	* * *  
	______ ______ ______

都會顯示成同一種分隔線：

> ---

# 區段元素
## 連結
Markdown的連結有兩種方式，一是行內，一是參考。兩種都是用`[]`來標記要形成超連結的文字。

### 行內連結
行內連結是用`[]`將文字包起來後，再加上`()`，並在小括號內加上連結網址即可。若想幫連結加上標題，也就是滑鼠移動到連結文字上會顯示的標題，在小括號內的連結網址後，空一格，用`"`將標題文字包起來即可。

例如：

	`This is a [sample](http://example.com/ "example.com").`

就會呈現為：

> This is a [sample](http://example.com/ "example.com").

### 參考連結
若你的文章內有多處要連結到同一個網址連結，則用參考連結是較好的方式。

參考連結一樣是用`[]`將文字包起來，後面再用一次`[]`將用來辨識連結的標籤包起來。例如：

	`Let me [Google] [0] that for you.`

同樣會呈現為：

> Let me [Google] [0] that for you.

然後在文件的任意處，對，「任意處」，放上標籤內的連結內容定義，例如：

	`[0]: http://www.google.com/ "Google"`

但很抱歉，這個參考連結的內容定義並不會實際呈現出來，想檢查正確與否，就是直接點超連結的文字來測試。

而連結的內容定義，有一定的語法，所以有以下幾點需要注意：

* `[]`內輸入連結的辨識標籤，可以是字母、數字、空白和標點符號，但並無大小寫區分
* `[]`後必須接一個`:`，再接著一個以上的空白或縮排 tab
* 空白或縮排 tab後再接連結網址，可以選擇用`<>`將網址包起來，但非必要
* 網址後面可以選擇性地加上連結標題，也就是滑鼠游標移到超連結文字上後會顯示的標題，須用`''`、`""`或`()`包住標題

## 強調
將想要強調的文字用`*`或`_`包起來，就可以呈現三種強調的方式。例如：

	***粗斜體***  
	__粗體__  
	*斜體*

會呈現如下：

> ***粗斜體***  
> __粗體__  
> *斜體*

## 程式碼
這邊跟程式碼區塊的區別，是只用來標記一小段行內程式碼，直接用`` ` ``將程式碼包起來即可。例如：

	`` `This is a code.` ``

就會顯示為：

`This is a code.`

若程式碼內有需要用到`` ` ``這個符號，可以用多個`` ` ``符號來包住程式碼以作區別，例如：

```
	A single backtick in a code span: `` ` ``  
	A bakctick-delimited string in a code span: `` `foo` ``
```

就會顯示為：

> A single backtick in a code span: `` ` ``  
> A bakctick-delimited string in a code span: `` `foo` ``

## 圖片
插入圖片的 Markdown語法跟連結非常相似，幾乎只差在需要在開頭加上一個`!`符號。例如：

	`![Markdown logo](https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/208px-Markdown-mark.svg.png "Markdown")`

就會顯示出圖片：

> ![Markdown logo](https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/208px-Markdown-mark.svg.png "Markdown")

行內圖片的語法注意如下：
* 須以一個`!`開頭
* 接著以`[]`加入替代文字，也就是圖片路徑、網址失效的時候顯示的文字
* 再以`()`加入圖片路徑或網址
* `()`內的網址後面，只可以`''`或`""`包住可以選擇加上的標題

參考圖片的語法則像這樣：

	`![Evernote logo][1]`

參考的定義方式則與連結的參考內容定義方式一模一樣：

	`[1]: https://upload.wikimedia.org/wikipedia/en/thumb/8/87/Evernote-logo.svg/200px-Evernote-logo.svg.png "Evernote"`

同樣可以顯示出圖片：

> ![Evernote logo][1]


# 其他
## 自動連結
Markdown也支援比較簡短的連結形式，可以用來表達連結網址及信箱，同時也能有超連結功能，只需要用`<>`包住網址即可。例如：

	`<http://example.com/>`

就可以顯示為：

> <http://example.com/>

## 跳脫字元
前面講了很多 Markdown的語法，使用很多符號來達成指定功能的標記，那如果只是需要在文章中加入那些符號，但並不想使用相關的功能，就需要在該符號前面加上`\`這個符號，以達成跳脫字元的功能。

例如：

	`If I want to \*\*emphasize\*\* something without making it **bold**.`

就會顯示為：

> If I want to \*\*emphasize\*\* something without making it **bold**.

以下是 Markdown支援能在前面加上`\`以形成跳脫字元的符號：

> `\` 反斜線  
> `` ` `` 反引號  
> `*` 星號  
> `_` 底線  
> `{}` 大括號  
> `[]` 中括號  
> `()` 小括號  
> `#` 井字號  
> `+` 加號  
> `-` 減號  
> `.` 英文句點  
> `!` 驚嘆號

## 特殊功能
前面都是介紹 Markdown原生支援的語法，其實有很多通用的寫法也能適用在 Markdown當中。這邊列出我找到的一些語法，但請注意使用的編輯器或轉換器的支援度。

### Checkbox
語法是先用一個`-`，一個空格，再加上`[ ]`，空格後再加上敘述。注意`[ ]`當中必須有一個空格。若需要顯示的 checkbox已經勾選，請將`[ ]`當中的空格替換成`x`或`X`。

例如：

	- [ ] First box

就會顯示為：

> - [ ] First box

### Table
Markdown其實也支援做表格，基本上需要三個部分，標題列、設定列、內容表格。基本上都是用`|`做為分隔符號。

例如：

	No.|Pokemon|神奇寶貝  
	:---:|:---|:---  
	1|Bulbasaur|妙蛙種子  
	2|Ivysaur|妙蛙草  
	3|Venusaur|妙蛙花

會顯示為：

> No.|Pokemon|神奇寶貝  
> :---:|:---|:---  
> 1|Bulbasaur|妙蛙種子  
> 2|Ivysaur|妙蛙草  
> 3|Venusaur|妙蛙花

在畫表格的時候，有幾項注意事項：

* 左邊界跟右邊界的框線非必要
* 標題列必須每欄都填入欄位名稱
* 第二列設定列，每一欄都必須填入至少一個`-`符號，並用`:`設定對齊方式。預設是靠左對齊；`:-`也代表靠左對齊；`-:`代表靠右對齊；`:-:`則代表置中
* 內容表格必須至少一列

## 支援程式碼
這邊特指的是程式碼區塊。

其實大家應該注意到前面的程式碼區塊的文字有各種顏色，其實就是 Markdown在做辨識程式語言的工作，並試圖將跟辨識出來的語言的關鍵字做顏色標記。

如果記錄在程式碼區塊的程式碼有確切的語言，不仿試用以下的辦法，讓 Markdown能更好的辨認程式碼，並更好地標記。

首先必須使用三個`` ` ``來前後包住程式碼區塊，然後在第一排`` ` ``的後面加上程式語言名稱。

例如：

```
	```java  
	public static void main(String[] args) {  
	System.out.println("Hello World!");  
	}  
	```
```

就可以讓 Markdown辨識如下：

```java
public static void main(String[] args) {
	System.out.println("Hello World!");
}
```
另外，利用這個辨識的功能，還能延伸為繪製一些簡單的圖表，如流程圖。

詳細語法請上網搜尋`markdown`加`flow`。這邊僅舉例：

	```flow
	st=>start
	op=>operation: operation
	con=>condition: condition
	e=>end
	
	st->op(right)->con
	con(yes)->e
	con(no)->op
	```
Markdown辨識後，會自動繪圖如下：

> ```flow  
> st=>start  
> op=>operation: operation  
> con=>condition: yes or no?  
> e=>end  
> 
> st->op(right)->con  
> con(yes)->e  
> con(no)->op  
> ``` 

（很顯然 Hugo提供的轉換器並不支援這種擴充的繪圖功能）

[0]: http://www.google.com/ "Google"
[1]: https://upload.wikimedia.org/wikipedia/en/thumb/8/87/Evernote-logo.svg/200px-Evernote-logo.svg.png "Evernote"