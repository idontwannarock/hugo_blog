---
title: "Git及 GitHub基礎認識"
slug: "git-and-github-basic-1"
date: 2017-09-14T07:13:01+08:00
draft: false
tags:
- Git
- GitHub
- SSH
- Git Bash
- Win10
- MacOS
categories:
- Programming
#disqusIdentifier: fdsF34ff34
keywords:
- github
- git
- ssh
- gitbash
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
# 學習目標
因為 Git指令一直出問題，今天就來搞清楚 Git跟 GitHub的各種問題吧！

# 學習內容

## Git跟 GitHub是什麼
[Git Wiki](https://zh.wikipedia.org/zh-tw/Git)則說 Git是一種分散式版本控制軟體。

詳細的說明可以參考[Git Documentation](https://goo.gl/YzDiHy)，有中文版，不過翻譯的只有前幾個主題。  

[GitHub Wiki](https://zh.wikipedia.org/zh-tw/GitHub)上說，GitHub是一個透過 Git進行版本控制的軟體原始碼代管服務，簡單來說就是可以放各種 Code的地方，但其實也可以放一些文件跟圖片等，好像沒有空間限制，只是有單一檔案大小 1GB的軟性限制。

### Git觀念
這裡我們來先解釋一下 Git版本控制的觀念，我覺得[寫點科普](https://hellolynn.hpd.io/)寫的這兩篇寫得非常平易近人而且完整，推薦給大家！

[GIT新手入門教學 – PART 1](https://hellolynn.hpd.io/2017/01/18/git%E6%96%B0%E6%89%8B%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8-part-1/)  
[GIT新手入門教學 – PART 2](https://hellolynn.hpd.io/2017/01/18/git%E6%96%B0%E6%89%8B%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8-part-2/)

我的理解是譬如有一份作業需要大家一起作，大家先把原始的作業文件(origin)放在小組長那邊(Remote)，然後各自 copy一份回家(Local)寫自己要做的部分，然後拿回去給小組長，由小組長決定誰的作業寫得好，可以成為新一代的原始作業文件(master)；或某人提交的作業寫得不完整，但寫過地那部分很好，就跟原始作業合併(merge)成一份新一代的原始作業文件。大家也可以 copy別人寫的作業回去修改(pull)，反正最後由小組長決定哪個版本的作業寫得最好，就可以成為新一代的原始作業文件這樣。

而大家 copy回家寫的作業也有三個階段，假如我在電腦上打作業，分成三個資料夾，一個是 Working Directory、一個是 Staging Area、一個是 Repository。

第一個資料夾就是放 copy回家的作業，然後我可能亂打了一些、新增修改了一些，但交出去很丟臉的部分；第二個資料夾就是放某些我覺得可以的部分作業，先暫時存起來；最後一個資料夾就是放我確定要提交的作業版本。

所以我寫作業的流程就是這樣：

1. 先 copy一份(pull)原始作業文件(origin)回家(local)
2. 在 Working Directory資料夾寫作業，找各種資料，新增刪減等等
3. 將比較滿意的部分暫存(add)到 Staging Area資料夾
4. 當 Staging Area資料夾有比較完整的作業版本後，一次整個儲存(commit)到 Repository資料夾中
5. 最後再將 Repository資料夾中要繳交的作業交出去(push)給小組長(remote)

## 建立 GitHub帳號
接下來說明實際操作流程。

建議大家先到 [GitHub](https://github.com/)建立自己的帳號，基本功能都是免費的，只有當你要發展私人專案，想要將 repositories設定為 private的時候會要收費的樣子。

GitHub帳號申請流程跟一般申請免費帳號一樣，就到首頁按下綠色的 Sign up for GitHub按鈕之後，一路照指示填上資料跟選擇選項就可以了。然後 GitHub應該會寄一封認證 email，請點 email裡面的 Verify email address那個連結來確認你的 email address。  
  
接下來先作 Git的環境設定，這樣之後就可以都在 Git Bash操作各種指令，不用在 Git Bash跟 PowerShell視窗換來換去。如果是 Mac用戶，則都可以用 MacOS隨附的「終端機」軟體，或安裝下載相同功能的 iTerm2來操作 Git指令。

## Git環境設定
先說明我一般使用的是 Windows 10，兼有一台 Macbook Pro。但我是超級初心者，所以 Linux我完全不會，抱歉。

先安裝 Git，這步驟很簡單。Windows就到 [Git官網](https://git-scm.com/) 下載就好，而且一鍵安裝，這邊不需要多講；若是 MacOS用戶，請利用 Homebrew安裝 Git，安裝 Homebrew跟 Git的操作過程可以參考我的[這篇文章](https://idontwannarock.github.io/hugo_blog/2017/11/my-mbp-environment-2017/#安裝Homebrew)，然後可以直接跳到下一個主題：設定 Git識別資料。

然後應該會在 Windows按鈕（狀態列左邊 Windows圖示的那顆）裡面的程式集多一個 Git的資料夾，裡面有三個程式：Git Bash、Git CMD跟 Git GUI。最常用的大概是 Git Bash，原則上都在這裡下各種 Git指令；Git CMD我不知道拿來幹嘛；Git GUI是圖形介面，但設計的不太好用。

如果大家沒有要學太多 Git指令，其實可以直接下載 [GitHub Desktop](https://desktop.github.com/)或 [Sourcetree](https://www.sourcetreeapp.com/)，圖形化介面真的太好用，也不用記一堆 Git指令。但今天沒有要教大家怎麼用 GitHub Desktop跟 Sourcetree，或其實大家看完後面 Git概念教學就大概會懂使用流程。

## 設定 Git識別資料
安裝完 Git之後，首先應該設定使用者名稱跟 email，應該要跟你之前申請 GitHub帳號時的 username及 email相同。

以下步驟使用到的指令，基本上在 Windows跟 MacOS上是一樣的，只有一些地方會有所不懂，我會特別說明。

請打開 Git Bash，可能在桌面就有，或者開始按鈕裡的程式集 Git資料夾裡面有，MacOS請打開終端機，然後依序輸入以下兩行 Git指令：  
    
    git config --global user.name "GitHub username"  
    git config --global user.email "GitHub email"
  
接著你可以輸入以下指令來檢查資訊是否有輸入正確。  
    
    cat ~/.gitconfig

## 建立 SSH Key並增加到 GitHub
SSH Key就像一個鑰匙，每一台電腦、筆電都會生成一個獨一無二的 SSH Key，然後我們上自己的 GitHub去登記這個鑰匙，這樣以後我們用電腦或筆電上傳東西到 GitHub時，電腦或筆電就可以用這個鑰匙，以及前面設定的 Git識別資料去開啟我們的 GitHub帳號並把東西上傳上去。

就跟我們要去銀行存錢，要提供身分證(Git識別資料)跟密碼(SSH Key)給銀行一樣。
  
要生成一個 SSH Key，一樣在之前打開的 Git Bash或終端機輸入以下指令：  
    
    ssh-keygen -t rsa -C "GitHub帳號的 email"
  
會出現以下這行，設定儲存 SSH Key的位置，使用預設的就好，所以直接按 Enter。
    
    Enter file in which to save the key (/Users/使用者名稱/.ssh/id_rsa): [Press enter]
  
如果你以前有設定過 SSH Key，它會出現這行`/Users/you/.ssh/id_rsa already exists. Overwrite (y/n)?`，建議直接打`yes`或`y`來重新操作以確保正確。接著會出現以下這行來問你是不是要為 SSH Key設定一個密碼，要就輸入，並且會需要再輸入一次作確認，不要就直接 Enter。
    
    Enter passphrase (empty for no passphrase): [Type a passphrase]
  
然後他就會顯示一大段文字，表示 SSH Key產生成功，接著我們把 SSH Key加到 ssh-agent來免除每次要連接登入 GitHub都還要再輸入一次 SSH Key的密碼。請先輸入以下指令：  
    
    eval $(ssh-agent -s)
      
接著會出現這行`Agent pid 8492`，數字每個人都不一樣，這沒關係。接著輸入以下這行，可能會需要重新輸入一次 SSH Key的密碼：  
    
    ssh-add ~/.ssh/id_rsa
  
如果出現`Identity added`這行字就表示成功了。

再來需要把 SSH Key加入到自己的 GitHub帳號。  
  
首先在同樣的 Git Bash畫面輸入以下這行，將 SSH Key複製到剪貼簿裡面，就類似平常按`Ctrl`+`C`那樣複製。  
    
    clip < ~/.ssh/id_rsa.pub

如果是 Mac使用者，請到`/使用者名稱/.ssh/`這個資料夾，若找不到請調整隱藏檔的設定，然後用文字編輯打開`id_rsa.pub`這個檔案，講整個檔案內容複製起來。

然後用瀏覽器進入到你自己的 GitHub帳號，點最右上角的三角形，選 Settings，然後選左邊列表的 SSH and GPG keys，點綠色的 New SSH key，然後在 Key下面的欄位直接`Ctrl`+`V`或`command`+`V`把 SSH Key貼上，在 Title欄位輸入你之後能辨識這個 SSH Key是代表哪一台電腦或筆電的名稱，最後點綠色的 Add SSH key按鈕就添加完成啦！  
  
然後作個小測試，在同樣的 Git Bash或終端機輸入`ssh -T git@github.com`，可能會看到類似以下的一段文字：  
    
    The authenticity of host 'github.com (207.97.227.239)' can't be established.  
    RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.  
    Are you sure you want to continue connecting (yes/no)?
  
fingerprint後面那一串長長的字每個人都不一樣，這也沒關係。輸入`yes`後應該會跳出以下訊息：  
    
    Hi username! You've successfully authenticated, but GitHub does not provide shell access.
  
這段文字中的 username是你 GitHub設定的 username，這樣就代表成功啦！

## 建立 Project並上傳到 GitHub
接下來利用建立一個新專案來介紹一些 Git的基本指令。

首先先到桌面或隨便一個資料夾，建立一個 test資料夾，然後在資料夾裡面隨便新增一個文字檔案，~~公堂之上假設一下~~ 假設就叫`first-post.md`（md檔案是 Markdown語言的檔案，內容可以被 GitHub直接讀取並且辨識），接著請在 test資料夾內的空白處點右鍵，選 Git Bash Here，就會打開 Git Bash，並預設路徑就是 test資料夾。

如果是 MacOS使用者，也請建立一個資料夾，並同樣新增一個`first-post.md`文字檔案，請對該資料夾按一下右鍵或`control`鍵出現選單，再按著`option`鍵，會出現`拷貝「資料夾名稱」作為路徑名稱`的選項，選擇之後就會複製資料夾路徑。然後開啟終端機輸入`cd`，然後空一格貼上剛才複製的路徑，以移動操作位置到該資料夾，很重要，請一定要做。
    
    cd 資料夾路徑

接著就要開始操作 Git指令，如果覺得我講的不清楚，可以回去看寫點科普那兩篇文章的觀念跟操作。

這邊還是記錄一下我的作法。請大家，不論是 Windows或 MacOS使用者，都輸入以下命令：
    
    git init
  
init就是 initialize，這代表將這個資料夾變成一個 Repository，Git就會開始記錄這個 Repo裡面的所有改動跟版本。然後以下指令會新增全部 test資料夾裡面的檔案到 staging的狀態。  
    
    git add .

staging好了之後，再用下面這個指令來 commit到本機的 Repo，這些 commit到 Repo的東西才能被 push到 GitHub上。  
    
    git commit -m "說明操作了什麼的一段文字"

這過程中隨時都可以用`git status`指令來查看你處於哪個階段。  

最後要 push到 GitHub之前，請先到 GitHub上建立一個名稱為 test的 Repository，建立好之後，請點中間 SSH那個按鈕，後面會生成該 Repo的 SSH url，把那個網址複製下來。若建立 Repo的時候有勾 README選項，則按右邊綠色 Clone or download按鈕，點藍色 Use SSH連結切換到 Clone with SSH，再複製 url。  

最後一樣到剛才的 Git Bash或終端機裡面輸入以下命令，我們要將 commit push到 GitHub上。過程中可能會要輸入 SSH密碼。  
    
    git remote add origin git@github.com:GitHub使用者名稱/test.git  
    git push origin master

第一句是要為這個專案加上 GitHub上面 Repo的位置，後面要 push，Git才知道要 push到哪裡。第二句話就是把已經 commit的版本 push到 GitHub對應 Repo的 master分支上。master也就是主要版本。

這樣就完成建立一個新 Project並上傳到 GitHub啦！

## push修改過的 Project到 GitHub
最後，如果之後要修改剛建立的那個 Project資料夾裡的任何內容，想要再把變更 push到 GitHub上，請在 test資料夾打開 Git Bash，或終端機照前面說明移動位置到該資料夾下，輸入以下指令：  
    
    git add .  
    git commit -m "說明文字"  
    git push origin master

就很簡單的搞定啦！  

至於 branch那種東西，等我搞懂再來新增吧。今天先這樣~~