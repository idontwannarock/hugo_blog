---
title: "我在Macbook Pro的設置 - 2017版"
date: 2017-11-03T09:05:02+08:00
draft: false
tags:
- Mac
- brew
- cask
- zsh
- oh my zsh
categories:
- Personal
- Software
#disqusIdentifier: fdsF34ff34
keywords:
- Mac setup
- brew
- cask
- zsh
- oh my zsh
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
一直以來都是 PC人，從來沒用過任何 Apple或 Linux的相關產品，剛好有買筆電的需求，想趁機接觸一下不同的作業系統生態，而且久聞 Apple筆電品質很好，就添購了 Macbook Pro來當我人生第一台筆電。

剛拿到筆電總是需要一些設置，盡量讓 PC跟 MBP之間資訊同步以及應用軟體上相通或相容，以達到同步並簡化作業環境的目標，提高生產效率。

於是跟朋友詢問以及上網稍作了解後，有了以下的設置。

# 軟體環境設置
因為是要習慣 Unix-based的作業環境，所以我並沒有特別強求各方面都要設置到跟 Windows環境類似，所以操作模式上並沒有更動。

但安裝的軟體上就有些考量，希望能達到集中管理，這就不得不提每個 MacOS都應該必備的 Homebrew。

## 安裝 Homebrew
[Homebrew](https://brew.sh/)是一套開源的 MacOS系統的軟體套件管理系統，用來簡化 MacOS系統上的軟體安裝、卸載等過程，是用 MacOS內建的 Ruby語言寫成。

但 Homebrew在安裝前需要先安裝 [Xcode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12)，似乎是因為 Xcode會一併安裝一些常用的 command line。

還好 Xcode也是免費軟體，可以直接透過 App Store下載，要注意檔案蠻大的，下載安裝的過程會要花一點時間。

Xcode安裝好之後，就打開「終端機」，輸入下面這行來下載安裝 Homebrew：

```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

注意第一個`$`是開啟終端機就會顯示在你可以打字的那一行的開頭，不用重複輸入。

讓他自動跑完之後，就可以開始使用`brew`指令來操作啦！

日後要更新 Homebrew這個軟體本身，也是一樣在終端機輸入`brew update`以及`brew tap homebrew/dupes`就可以了。

## 安裝 Caskroom
除了 Homebrew以外，第二個推薦安裝的就是 [Caskroom](https://caskroom.github.io/)，這也是一個軟體套件管理系統，是 Homebrew的擴充。

一般來說 Caskroom主要用來下載安裝一些有操作介面的應用軟體，譬如 Chrome、Spotify、Evernote等等；Homebrew則常用於下載安裝一些沒有操作介面的工具或第三方資源，例如 Git、Hugo、Telnet這種。

Caskroom可以看成 App Store的擴充，並附帶自動安裝管理的功能，而且因為也是開源專案，它能安裝的軟體是由開放社群中的使用者提供維護，有很多 App Store沒有的軟體，當然是正版、免費版或試用版。

而且 Caskroom還有**更新管理**的功能，除非軟體自帶自動更新功能，否則可以透過 Caskroom統一更新。所以一般來說，Homebrew更偏開發者使用，Caskroom則更適合一般使用者。

而 Caskroom的安裝也很簡單，安裝過 Homebrew後，只需要輸入以下這行就可以安裝好 Homebrew：

```
$ brew install caskroom/cask/brew-cask
```

## 使用 Homebrew及 Caskroom
這兩個軟體的指令都很類似而且很容易，Homebrew就是指令前面加上`brew`，Caskroom就是`brew cask`。

然後共通的常用指令就是`install`安裝、`uninstall`解安裝、`info`查詢軟體資料以及`list`列出已安裝軟體，一樣都是前面加上`brew`或`brew cask`，然後加上選擇的指令，最後再加上軟體名稱。

Caskroom還有一個很好用的功能`search`，也就是你輸入`brew cask search xxx`，它會搜尋比對已安裝、未安裝的軟體名稱，未安裝的軟體名稱還會分成完全相同(Exact Match)以及部份相同(Partial Matches)兩部份，讓你選擇需要的軟體來安裝。

## 我的安裝列表
這邊列出我的安裝列表，都是一些我覺得在 MacOS上，很通用、方便的軟體跟功能，提供給大家參考：

    * Homebrew *
    git             // 開發版本管理工具
    hugo            // 靜態網站生成器
    telnet          // 上 ptt用環境設置
    
    * Caskroom *
    google-chrome   // 上網必備
    appcleaner      // 好用的刪除軟體工具
    istat-menus     // 顯示系統資訊，可以在桌面頂部的資訊列顯示上下傳速度、電池狀況、CPU溫度等等資訊
    sourcetree      // Git的圖形化介面軟體
    iterm2          // 更好用的終端機，可以多開分頁！
    spotify         // 聽音樂，不解釋
    moom            // 讓 Mac可以調整最大化視窗的位置
    cheatsheet      // Mac快速鍵指令表
    the-unarchiver  // 增強解壓縮功能的工具
    vlc             // 強悍影音播放程式
    evernote        // 資訊管理、筆記軟體，跨平台超好用，重點還可以 web clip存網頁
    welly           // 上 ptt用軟體
    xmind           // 心智圖軟體

當然每個人都有不同的偏好，其中有些也有很好的替代軟體，像是 Welly就有相同功能的 Nally，再加上 PTT最近基於 [PttChrome](https://iamchucky.github.io/PttChrome/)，採用實驗性的 Websocket連線而推出一個新的服務，直接在瀏覽器輸入`term.ptt.cc`就可以直接上PTT，不用額外安裝任何軟體或插件，讓 Welly跟 Nally對我來說幾乎就要淘汰(攤手)。

詳情可參考這篇公告：[\[公告\] 使用瀏覽器直接連線至批踢踢](https://www.ptt.cc/bbs/SYSOP/M.1508496102.A.17E.html)

另外，因為 Homebrew跟 Caskroom的安裝指令都要在終端機或 iTerm2這類 CLI軟體上輸入指令，厲害的人可以把你有安裝的軟體，每一條指令合起來做成 .sh檔，這樣如果有需要重灌系統，只要執行一遍 .sh檔，所有軟體就可以一次性的安裝回來啦！

### Honorable Mention: oh my zsh
這邊想推薦的是對常用終端機類 CLI軟體的使用者或開發者比較有用的東西，所以不常用或對 CLI沒興趣的讀者直接跳過這段吧！

在說明 oh my zsh之前，要先簡單說明，也是記錄一下什麼是 zsh。

但在說明 zsh之前要再說明一下什麼是 shell(跪)。

shell是一種泛稱。在 Unix-based的作業系統，例如 Linux或 MacOS中，shell就是指用來跟系統核心(kernel)溝通的工具，kernel收到 shell傳來的指令後，會解析成各種電腦看得懂的指令，然後交給 CPU或其他有關的電子元件做資料處理，kernel的簡單說明可以參考 [wiki](https://zh.wikipedia.org/zh-tw/內核)。

zsh(z shell)也是一種 shell，但 Unix-based的作業系統默認的 shell是 bash，總之都是一種 shell。

而 zsh的好處就在於比預設的 bash有更多、更方便的指令，例如忘記完整指令，只要輸入指令前幾個字，按`tab`鍵，zsh就會幫你列出所有選項，再按一次`tab`鍵就可以切換到選擇模式，在列出的指令列表中選擇要執行的指令，光這點就不用選了，就是 zsh了！

然後講到 oh my zsh，這是一套基於 zsh的框架，也就是提供更進階的功能，身為剛入門的開發者，我覺得它最大的好處就是彩色化！oh my zsh可以安裝 themes，各種 themes會對許多常用的關鍵字做不同的彩色化等等的處理，這樣用純文字畫面的 CLI時，就可以更清楚的區分畫面上的資訊！

#### 安裝設置 oh my zsh
基本上 MacOS都已經預設安裝好 zsh，所以不用我們安裝，所以直接安裝 oh my zsh就好。

要安裝 oh my zsh，請打開任一 CLI，輸入以下這行指令就可以自動下載並安裝：

```
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyryssell/oh-my-zsh/master/tools/install.sh)"
```

安裝好 oh my zsh之後，預設就會有主題，對初學者的我來說夠用，但如果你想做調整，就要到`MacOS帳號名稱`資料夾的隱藏檔案中尋找`.zshrc`檔案，這就是 oh my zsh的設定檔，所有東西都可以在這邊設置。

這聽起來很麻煩，但用過就會像變心的女朋友一樣，回～不～去～啦～～～

# 工作環境設置
接下來講到工作環境設置。

因為在學習網頁前後端開發，會用到 [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)、[Eclipse](https://www.eclipse.org/downloads/packages/eclipse-ide-java-developers/oxygen1a)、[Brackets](http://brackets.io/)等等，也會寫一些筆記存到 [Evernote](https://evernote.com/)，或例如這篇的靜態部落格文章。

但我常常會交替在 MBP跟 PC上進行開發或筆記的工作，要怎樣保持 MBP、PC，甚至手機上都能同步到最新進度，對初學者的我，是花了一番心思。

## 開發同步
首先講純開發的部分，比較簡單，前面提到的開發軟體或環境一樣都可以利用 Homebrew或 Caskroom下載安裝。

接著就是利用 [Sourcetree](https://www.sourcetreeapp.com/)跟 [GitHub](https://github.com/)來做 Git版本管理同步。

所有專案、檔案，都透過 Sourcetree push到 GitHub的 repositories。然後每個裝置要編輯開發前，都先 pull Github上的最新進度，這樣就可以簡單的保持各裝置開發進度相同。

當然，使用 Sourcetree會需要一些 Git觀念。有關 Git的簡單觀念及操作，可以參考我寫的[這一篇文章](https://idontwannarock.github.io/hugo_blog/2017/09/git-and-github-basic-1/)。

## 筆記同步
這部分比較麻煩一點，因為我習慣統一用 Markdown語法寫筆記跟部落格，這樣規格統一，筆記跟部落格文章可以很方便地互相轉換。

Markdown簡介跟語法可以參考我的[這一篇文章](https://idontwannarock.github.io/hugo_blog/2017/10/markdown-syntax/)。

而我的筆記都習慣收在 Evernote，這樣可以隨時利用 Evernote的分類以及搜尋功能，並且手機上也可以看。但要將 Markdown筆記轉成 Evernote讀得懂的格式並上傳到 Evernote並不是很容易。

之前是選擇用 Sublime Text加上開源的 Plug-in來轉換並上傳，但最近 Evernote將 developer token的功能停止之後，這個方法就不能再使用了。

於是我換到 [Marxico](https://marxi.co/)，其實算是相當方便，只是要收費，但在找不到更好的替換工具之下，也只能忍痛花下去。但好處就是我只要寫好 Markdown筆記，就可以很方便的上傳 Evernote，也可以匯出 Markdown、HTML，甚至是PDF檔。

另一方面部落格就真的很麻煩了，我原本只有 PC的時候，就是寫 Markdown草稿，然後用靜態部落格產生器 Hugo轉換並生成部落格，再 Host到 GitHub Pages來部署我的靜態部落格，可以參考我[這一篇](https://idontwannarock.github.io/hugo_blog/2017/09/hugo-practice-2/)。

但這個方法的問題就是無法多部裝置間同步，因為 push到 GitHub的只有 Hugo生成的`public`資料夾，而不是整個包含 layout跟 Markdown原稿的完整資料夾，所以換一部裝置就要用很麻煩的方式另外傳送整個資料夾。

於是我嘗試了別的方法。

### GitHub Pages
在講解我的方法之前，要講一下 GitHub Pages提供的託管靜態網頁服務分成兩種形式：**個人或組織主頁(User or Organization Page)**以及**專案主頁(Project Page)**。

差別在於個人主頁就是**一個 GitHub帳號只會有一個個人主頁方式的靜態網頁**，網址會是`https://<GitHub帳號>.github.io`；而**一個 GitHub帳號則可以有數個專案主頁**，網址原則上應該就是`https://<GitHub帳號>.github.io/Repo名稱`這樣。

當然，只要是專案主頁方式，網頁的網址就可以透過在 Repo根目錄生成 CNAME檔案，並記錄申請的域名來替換，這邊不多說。

### 部署 Hugo產生的靜態網頁到 GitHub Pages
我之前裡選擇的方式是專案主頁，因為我想保留個人主頁做我個人的履歷主頁，放置我的資訊跟 Porfolio之類的，所以 Blog就不能用個人主頁的方式部署在 GitHub Pages。

這便順便記錄一下，個人主頁其實部署方式跟專案主頁沒有太大差別，主要的差別在於個人主頁的 Repo名稱必須取為`<GitHub帳號>.github.io`，也就是跟個人主頁的網址相同；而專案主頁的 Repo名稱則沒有限定。

而 GitHub Pages的部署方式有三種，如同[官網說明](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/)。

#### Default Source Settings
第一種參考官網說明[這一段](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#default-source-settings-for-repositories-without-the-username-naming-scheme)。

就是我之前用的方式，在[這一篇](https://idontwannarock.github.io/hugo_blog/2017/09/hugo-practice-2/)裡有說明。

簡單來說，就是將 Hugo預設產生的`public`資料夾，直接 push到 GitHub的 Repo，GitHub預設會直接讀取 Repo中的檔案生成靜態網站。

#### Publish From a `docs` Folder on `master` Branch 
第二種要做比較多設定，參考官網[這段](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#publishing-your-github-pages-site-from-a-docs-folder-on-your-master-branch)。

因為 GitHub Pages有提供另一種部署方式，就是它可以選擇讀取 Repo的`docs`資料夾內檔案來生成靜態網站，而不是第一種方式直接讀取 Repo根目錄裡的檔案。

所以我們先將 Hugo資料夾中的`config.toml`檔案用文字編輯器打開，在開頭加入以下這一行：

```
publishDir = "docs"
```

這是因為 Hugo預設生成靜態網頁的檔案會存在`public`資料夾，而這一行參數就是告訴 Hugo將生成的靜態網頁檔案改存在`docs`資料夾。

然後一樣將整個 Hugo資料夾 push到 GitHub上，然後開啟瀏覽器進入那個 GitHub Repo，選擇 Repo名稱底下那排最右邊的 Settings，然後往下拉到倒數第二個區塊 GitHub Pages，在 source那邊的下拉選單選擇`master branch/docs folder`，然後點擊`save`就完成部署了。

這個時候 source上方應該會出現一行綠色底的文字，註明生成的網址，點進去就是實際生成的靜態網站。

往後寫新的文章就可以不用更動任何設置，直接用 Hugo指令生成後 push到 GitHub上就好。

然後不同裝置要保持同步也很簡單，就直接將整個 Repo從 GitHub上 pull或 clone下來，因為所有的設定檔案、layout、Markdown原稿都已經存在 GitHub上。

#### Publish from `master` or `gh-pages` Branch
第三種方式就難了，可以參考官網[這段](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#enabling-github-pages-to-publish-your-site-from-master-or-gh-pages)了解概念。

這種方式要對 Git有比較深入的了解，我也還沒全部弄懂 Git部分的操作過程。

但原理似乎大概是這樣，但**我不是非常確定**：

同樣利用 Hugo預設生成靜態網頁檔案到`public`資料夾，然後利用 Git branch的功能，產生一個`gh-pages`的分支版本，所以在 local，也就是操作的電腦上就會有`master`跟`gh-pages`兩個不同版本的檔案紀錄。

在`master`這個分支上利用 gitignore屏蔽掉`public`資料夾，然後將其他所有檔案 staging -> commit -> push到 GitHub Repo的`master`分支。

再切換到`gh-pages`這個分支上，將除了`public`資料夾以外的所有檔案都用 gitignore屏蔽掉，然後一樣將`public`資料夾 staging -> commit -> push到 GitHub Repo的`gh-pages`分支。

這時候 GitHub的 Repo上就同樣有`master`跟`gh-pages`兩個不同版本的紀錄。

然後開啟瀏覽器進入 GitHub Repo，同樣選擇 Repo名稱底下那排最右邊的 Settings，然後在 GitHub Pages區塊的 source下拉選單裡選擇`gh-pages branch`，然後點擊`save`就完成了。