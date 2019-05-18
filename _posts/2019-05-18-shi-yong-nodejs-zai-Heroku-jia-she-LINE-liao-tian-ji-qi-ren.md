---
layout: post
title: "使用 node.js 在 Heroku 架設 LINE@ 聊天機器人"
author: patrick
categories: [Heroku]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/line_bot/heroku-node-1.png"  
---

Node.js 是一個能夠在伺服器端運行 JavaScript 的開放原始碼、跨平台 JavaScript 執行環境。它有自己的一系列的模組，所以可以讓他脫離 apache2、nginx 或 IIS，可以獨立運作，而且運行的效能是非常強

### 先建立 node.js 的環境

node.js 的環境，在這裏就不多說廢話，請參考下面的網址

如果是 Mac，請先安裝 Homebrew，直接按照 [Homebrew 的官網](https://brew.sh/index_zh-tw.html) 說明即可

- Windows 使用者：[第一次建置node.js開發環境和安裝npm就上手！](https://ithelp.ithome.com.tw/articles/10199058)
- Mac 使用者：[node在osx開發環境設置: 一次釐清brew,nvm, npm,node](https://weitinglin.com/2018/01/31/node%E5%9C%A8osx%E9%96%8B%E7%99%BC%E7%92%B0%E5%A2%83%E8%A8%AD%E7%BD%AE-%E4%B8%80%E6%AC%A1%E9%87%90%E6%B8%85brewnvm-npmnode/)

### 開始建立 node.js 

直接開啓一個空白路徑，假設 ~/line-bot 就好了

```
cd ~
mkdir line-bot
cd ./line-bot
```

接着跑下面的指令，一直按下 Enter 直到結束

```
npm init
```

你會得到 package.json，等下再處理它

直接跑下面的 install，安裝它的套件，因爲是 LINE 機器人，所以要安裝 linebot 套件

順便安裝 express，用來處理傳遞與接收訊息 

```
npm install linebot
npm install express
```

### 開始寫 app.js

直接開始寫 app.js，讓他可以直接跑起來

```
const linebot = require('linebot');
const express = require('express');

const bot = linebot({
    channelId: '你的 LINE Channel ID',
    channelSecret: '你的 LINE Channel secret',
    channelAccessToken: '你的 LINE Channel access token'
});


//這一段的程式是專門處理當有人傳送文字訊息給LineBot時，我們的處理回應
bot.on('message', function(event) {
    if (event.message.type = 'text') {
        let msg = event.message.text;
        //收到文字訊息時，直接把收到的訊息傳回去，這裏是 echo，就是你問什麼就回答什麼，簡單的對話
        event.reply(msg).then(function(data) {
            // 傳送訊息成功時，可在此寫程式碼
            console.log(msg);
        }).catch(function(error) {
            // 傳送訊息失敗時，可在此寫程式碼
            console.log('錯誤產生，錯誤碼：'+error);
        });
    }
});

const app = express();

// bot.parser() 是 LINE Bot 的傳過來的資料，以及 JSON 解析
const linebotParser = bot.parser();
app.post('/webhook', linebotParser);

const server = app.listen(process.env.PORT || 80, function() {
    let port = server.address().port;
    console.log('目前的port是', port);
});
```

### 針對 Heroku 做個設定

這裏是用 Heroku 當作 webhook 的連結

在自己的開發資料夾底下，開啓 Terminal

```
// 這是 Heroku 的登入，他會啓動瀏覽器，照着做就可以了
heroku login
```

記得先建立起 .gitignore，這是忽略底下的內容

如果你使用的 IDE 的 PHPStorm 可以吧 .idea 的設定進去，重點是 node_modules 一定要在裏面，否則你會跑很久

```
.idea/line_bot.iml
.idea/misc.xml
.idea/php-inspections-ea-ultimate.xml
node_modules/
```

然後就 git 下去

```
// 然後用 git，記得要設定 .gitignore
git init
git add .

// 這是下 comment
git commit -am "first commit"
```

底下是第一次用 remote 的方式與自己的 git 連在一起

```
heroku git:remote -a [你的 Web 或 App 名稱]
```

最後才是 push 給 Heroku

```
git push heroku master
```

### 然後 LINE 的部分

LINE 的部分，請參考 [如何可以取得 LINE 的 ID](https://www.prgpress.com/ru-he-qu-de-LINE-ID/)

然後在裏面可以找到 Channel ID, Channel secret，直接貼上去就可以了

還有自己的 webhook 的網址給貼上去，然後一定要架設 webhook，當然你可以自己取一個名稱就好了

```
app.post('/webhook', linebotParser);
```

這樣就完成了，雖然它只回應你所打的內容，不過可以做的方面有很多，譬如：天氣預報之類的都可以

如果要測試或者 Demo 的話，Heroku 的確是一個好幫手
