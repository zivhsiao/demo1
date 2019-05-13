---
layout: post
title: "PHPStorm 與 VSCode 比較"
author: patrick
categories: [開發工具]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/phpstorm-vscode.jpg"  
---

目前使用的是 PHPStorm，因爲它的功能強大，一般的編輯器是比不上的，尤其它支援 FTP, SFTP 上傳等，還有支援 Git，也因爲如此而選擇它的原因

前一段時間，有用過 VSCode，覺得還不錯，試着換換口味，不過又換回 PHPStorm 了，後面就會介紹兩者不同之處

### VSCode 快速的說明

它的確是一個很好的編輯器，可以用它的 Market Place 來擴充它的 Extension

編輯器可以透過 Extension 讓單純的編輯器可以改成程式編輯器，它也可以很快的完成程式部分

也可以去安裝界面來符合自己的習慣，這是它的編輯畫面

![vscode](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/vscode-editor.png)

這是 extension 

![vscode](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/vscode-extensions.png)


這裏就不在多說怎樣可以建置以及 Extension，如果要知道如何去安裝以及推薦的套件，請參考以下的連結

- [安裝 Visual Studio Code 與擴充套件設定](https://ithelp.ithome.com.tw/articles/10191357)
- [小克的 Visual Studio Code 必裝擴充套件（Extensions）私藏推薦](https://blog.goodjack.tw/2018/03/visual-studio-code-extensions.html)
- [推薦的 VS Code Extensions 整理(2019/2月更新)](https://medium.com/itsoktomakemistakes/vs-code-extensions-a453e5d1e926)


### PHPStorm

PHPStorm 是個 PHP 爲主的編輯器

它的畫面如下

![PHPStorm](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/phpstorm.png)

只有幾個地方，第一個是 Deployment 的畫面，可以使用 FTP、FTPS、SFTP 或 Local file 

建議使用 SFTP 比較好

![PHPStorm](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/phpstorm-sftp.png)

覺得比較重要的是它右下角有個 UTF-8，只要你的檔案的編碼是正確的就可以了

它的編碼是依照原來的編碼爲主，有時會在載入檔案的時候，除非是裏面的編碼會要你確認是否重新載入或者直接轉換

基本是用 RELOAD 就可以得到正確的編碼

![PHPStorm](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/file-reload.png)

有時變成編碼有些奇怪，只要拉下右下角可以選擇不同的編碼，選擇對的就好

不過至少它的編碼有錯誤的時候，會如同上圖一樣，是否要 RELOAD，所以應該也不會遇到編碼不正確的時候

![PHPStorm](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/phpstorm_vscode/file-encode.png)

爲何這樣做，是我開發的公司有 Utf-8、Big5、GB2312 的這樣的需求，所以要對我來說就要特別注意

### 編碼的不同之處，就是讓我換回 PHPStorm

而且當你改變編碼之後，它永遠都是改變的編碼，假設 Big5，永遠都是 Big5

而且編碼是依照檔案爲主，而且不會在整個 Project 都是相同的編碼

VSCode 下面的編碼，卻是所有的檔案編碼都一樣，也就是 Big5，結果所有的檔案都是 Big5，而且它不會記住你的選擇

這也是我放棄 VSCode 的原因，改回 PHPStorm

它基本有外掛 Plugins 可以安裝很多東西，與 VSCode 一樣可以去改造屬於自己的編輯器習慣

很多人說 VSCode 本來就是編輯器，與 PHPStorm 比較就不對了，但是寫出來就是給 PHP 的開發者瞭解，PHPStorm 好在哪裏