---
title: "在 Windows 使用 Git 指令"
date: 2021-02-24T10:07:47+06:00
draft: false

# post thumb
image: ""

# meta description
description: "Windows環境, 環境變數, PowerShell, git in windows"

# taxonomies
categories:
  - "blog"
tags:
  - "Programming"
  - "git"

# post type
type: "featured"
---

macOS 系統原生支援 bash 和 git，但 Windows 使用者需要自行安裝和設定 git。Windows 使用者使用 PowerShell 設定 git 環境，包含下載、安裝和配置環境變數。
<!--more-->


<br />  
<br />  

如果你是 macOS 系統，原生的 bash 跟 git 就有很好的相容性，甚至不必另行安裝就可以使用。但是如果是 Windows 的使用者，並且 PowerShell 版本不足的話，就必須要自行安裝 git 並設定，未來**才可以在殼層中以指令執行**。

對於 git 需求較少的使用者而言，也許 [Github Desktop](https://desktop.github.com/ "Github Desktop") (Github發行的 git 圖形化應用程式) 就已經足以應付你的使用習慣，但對於有心經營程式語言的同學，請**不要浪費時間在 [Github Desktop](https://desktop.github.com/ "Github Desktop") 上**，否則光是處理 Bug 就足以浪費你一整個週末了...，這絕對不是我經歷過的血淚史...。

<br />  
<br />  

* ##### 前言
* ##### 甚麼是環境變數
* ##### 下載 [git for Windows](https://git-scm.com/download/win "Download git for Windows")
* ##### 新增環境變數

<br />  
<br />  

### 前言
在 Windows 系統中，最常使用的殼層 (Shell)，除了過去熟悉的 cmd 命令提示字元，從 2016 年開源的 [Windows PowerShell](https://zh.wikipedia.org/wiki/Windows_PowerShell "Windows PowerShell") 成了近期的熱門工具。本篇文章就以 PowerShell 進行設定，讓你快速上手 git 在 Windows 系統下的應用環境。

<br />  
<br />  

### 甚麼是環境變數  

在撰寫任何專案時後，總是需要使用多項工具，若正在建立系統的資料庫，那也許你會使用 SQL、MongoDB 等工具；若正在撰寫部落格，那你也許會用到 Hugo。因此本篇文章以 git 為例子，未來如果需要設定任何工具，也可以舉一反三，將**工具加入環境變數後，就可以在 Windows 系統下的殼層中使用。**

<br />  
<br />  

### 下載 [git for Windows](https://git-scm.com/download/win "Download git for Windows")

<br />  

1. 下載相應版本[git for Windows](https://git-scm.com/download/win "Download git for Windows")
1. 安裝在適當路徑
1. 複製 bin 資料夾路徑

<br />  

##### 詳情請看

下載 [git for Windows](https://git-scm.com/download/win "Download git for Windows") 後，依據電腦系統選擇相應的版本，如果不知道電腦的系統類型，可以回到桌面對「本機」(我的電腦) 選擇右鍵中內容，查看「系統類型」。

下載並且執行安裝檔，安裝在預設路徑或者自定義路徑都無妨，但是建議存放在系統硬碟，以大部分 PC 的安裝習慣而言，系統硬碟應該會對應到 **C:**，例如我安裝的路徑就是在 **C:\git**。

安裝完成後點開 git，再進入 bin 資料夾 **(C:\git\bin)**，並且複製路徑。

<br />  
<br />  

### 新增環境變數

<br />  

1. 在桌面點選「本機」右鍵選擇「內容」
1. 系統進階設定
1. 點選「環境變數(N)...」
1. 在使用者變數單擊 Path → 編輯(E)...
1. 將 bin 資料夾的路徑貼上去


##### 詳情請看
先在桌面找到「本機」右鍵選擇「內容」、點擊「系統進階設定」進入系統內容，再來要注意上方有五個分頁，在第三個分頁中，可以在右下角的位置找到「環境變數(N)...」按鈕並點擊。

![image](https://reidpig8350.github.io/images/post/git_windows/1st.JPG)
![image](https://reidpig8350.github.io/images/post/git_windows/sysconten.JPG)

如上圖，環境變數分成兩種，在上的是「使用者變數」，只會在多個使用者中的其中之一作用。因此如果是公司電腦，或者研究室的資產，只要在使用者變數中新增就可以，**避免影響到同事或者學長，後果請自負**！當然如果要讓所有使用者都可以使用，除了要在下方的「系統變數」中新增之外，還要確定每個使用者都有安裝 git。

在使用者變數單擊 Path → 編輯(E)...，進入「編輯環境變數」後點擊「新增」，並且把稍早複製的 bin 資料夾路徑 (我的路徑是 C:\git\bin) 貼上去並且點選確定，就大功告成了！

![image](https://reidpig8350.github.io/images/post/git_windows/envariable.JPG)
![image](https://reidpig8350.github.io/images/post/git_windows/gitbin.JPG)

還是不能使用嗎？請記得重新開機！接著就可以開始管理專案的版本！


### 小結
設定環境變數，就相當於告訴系統你的工具放在哪裡，因此如果仔細看 bin 資料夾裡的檔案，其中 git.exe 就是這篇文章的主角，因此未來在任何 Shell 中使用 git 指令，**都相當於來到 C:\git\bin 資料夾中執行 git.exe**。

因此當你照著文章脈絡設定好的現在，也已經可以在 Windows 中執行 bash.exe 囉！未來再新增任何工具時，請記得一定要再回來複習一下，究竟該如何設定！

![image](https://reidpig8350.github.io/images/post/git_windows/bash.JPG)