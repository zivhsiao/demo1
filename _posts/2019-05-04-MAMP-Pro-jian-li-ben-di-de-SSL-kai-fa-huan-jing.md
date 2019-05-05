---
layout: post
title: "MAMP Pro 建立本地的 SSL 開發環境"
author: patrick
categories: [開發工具]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/mamp-pro-normal.png"  
tag: featured
---

MAMP Pro 我用了一段時間，因爲是本機測試使用，所以 SSL 的部分給它閒置在旁邊，最近爲了測試，才開始本機端的 SSL 如何去做設定

MAMP Pro 的安裝就不用多說了，也可以使用試用版本

直接進入主題，安裝完成之後，當然按下 + 去建立一個本機的 web server，紅色框的部分是建立一個 server 的設定都在上面可以看到

![mamp_pro](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/mamp-pro-start-screen.png) 

#### 開始 SSL 的部分

SSL 部分，可以看到一開始是沒有打勾的，當你按下「Create self-signed certificate」，會出現要存放的目錄，當你選擇之後，它的 SSL 就已經打勾，並且兩個檔案已經選擇好了

![mamp_pro](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/mamp-pro-ssl.png)

這時要對 Port，這裏是 Apache SSL 用的 Port 是 8890

接下來連線就要改成 https://yourdomain:8890

![mamp_pro](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/mamp-pro-port.png)

這時用 Chrome 看會出現不安全的連線

首先去 Safari 輸入你的網站，譬如：https://yourdomain:8890，這時會出現不安全的網站，只要確認網站的沒有問題的就可以了

![safari](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/safari_warning-1.png)

![safari](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/safari-warning-2.png)

按下參訪此網站就進入 https 的網站了，這時候就可以關掉 Safari

進入鑰匙圈，選擇登入，下方則選擇「憑證」，選擇你的網站，按下滑鼠右鍵，選擇「取得資訊」

![key-ring](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/key-ring.png)

出現如下圖的項目，要展開「信任」

![key-ring](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/ssl-not-trust.png)

使用此憑證時，下拉選擇「永遠信任」，然後離開的時候會要你輸入密碼，輸入完成就可以了

![key-ring](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/ssl-trust.png)

#### 最後在確認 Chrome 進入網站是否 SSL 不安全已經不見了

最後再用 Chrome 開啓網站，這時就沒有不安全的訊息提示了

![ssl confirm](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp-pro/already-ssl-trust-chrome.png)

收工完成了




