---
layout: post
title: "使用 Node.js 開發 Skype 機器人的介紹"
author: patrick
categories: [Skype 聊天機器人]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/talk-bot.png"  
---

### Skype 簡短的介紹

Skype 是一家全球性網際網路電話，它通過在全世界範圍內向客戶提供免費的高品質通話服務，採用點對點技術與其他用戶連接，可以進行高品質語音聊天。連線雙方網路順暢時，音質可能超過普通電話，正在逐漸改變電信業。

Skype 是網路即時語音溝通工具。具備 IM 所需的其他功能，比如影片聊天、多人語音會議、多人聊天、傳送檔案、文字聊天等功能。它可以免費高解析的與其他用戶語音對話，也可以撥打國內國際電話，無論固定電話、行動電話、小靈通均可直接撥打，並且可以實現呼叫轉移、簡訊傳送等功能。

好了，現在介紹 Skype Bot 的做法

### 首先，請先註冊 Microsoft Azure

註冊的方式可以參考 [不想花錢測Azure☁️? 手把手帶你免費體驗Azure及Azure介紹](https://ithelp.ithome.com.tw/articles/10201833)，就不用介紹了

裏面提到 NT 6300 已經改成 NT 6100 了

### 開始寫程式

Node.js 然後使用，可以參考 [使用 node.js 在 Heroku 架設 LINE@ 聊天機器人](https://www.prgpress.com/shi-yong-nodejs-zai-Heroku-jia-she-LINE-liao-tian-ji-qi-ren/)

這一開始需要下指令，一樣按下 Enter 就好

```
npm init
```

這裏需要安裝的套件如下

```
npm install dotnet
npm install path
npm install restify
npm install botbuilder
```

還有 .env，它的 PORT 是使用 80

```
MicrosoftAppId=xxxxx-yyyyyy
MicrosoftAppPassword=xxxxxyyyyyy
PORT=80
```

然後記得要把 .gitignore 建立起來，裏面只有 node_modules 要讓 git 忽略這個目錄，因爲它不用加在 git

前置檔案已經處理好了

### 開始寫程式

一開始寫 app.js

```node
const dotenv = require('dotenv');
const path = require('path');
const restify = require('restify');

// 載入重要的 Bot 的檔案
const { BotFrameworkAdapter } = require('botbuilder');

// 引入 bot.js
const { EchoBot } = require('./bot');

// 載入 bot 的設定檔
const ENV_FILE = path.join(__dirname, '.env');
dotenv.config({ path: ENV_FILE });

// 建立 http 的 server
const server = restify.createServer();
server.listen(process.env.port || process.env.PORT || 3978, () => {
    console.log(`\n${ server.name } listening to ${ server.url }`);
});

// 建立一個連結器
const adapter = new BotFrameworkAdapter({
    appId: process.env.MicrosoftAppId,
    appPassword: process.env.MicrosoftAppPassword
});

// 所有錯誤發生的截取
adapter.onTurnError = async (context, error) => {
    console.error(`\n [onTurnError]: ${ error }`);
    // 錯誤訊息的產生並且發送出去
    await context.sendActivity(`Oops. Something went wrong! ${ error }`);
};

// 建立主要的 bot
const bot = new EchoBot();

// 監聽收到的訊息
server.post('/api/messages', (req, res) => {
    adapter.processActivity(req, res, async (context) => {
        // 讓主要的 bot 去跑文字的解析
        await bot.run(context);
    });
});
```

接下來是 bot.js

```node
const { ActivityHandler } = require('botbuilder');
const cheerio = require('cheerio')

class EchoBot extends ActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            
            textResult = `回應你的訊息：${ context.activity.text }`

            await context.sendActivity(textResult);

            await next();
        });
    }
}

module.exports.EchoBot = EchoBot;

```


這裏展示的很簡單，當你輸入「World Hello」，馬上回應你的
是「回應你的訊息：World Hello」

### 最後結果

Skype Bot 是架在 Microsoft Azure 底下

所以訊息端點就用 Heroku 來進行

只要改爲你的 Heroku 的網址，後面接上 /api/messages 就好了

記得使用「在 WebChat 中測試」看看是否好了 

