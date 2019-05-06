---
layout: post
title: "Facebook Messanger 聊天機器人的詳細說明"
author: patrick
categories: [Laravel, Lumen]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/WITAI_logo.png"  
---

這次是由 Facebook Messanger 的兩篇文章作爲參考 [LINE & FB Messenger 結合 wit.ai 來處理使用者發問的問題](https://www.prgpress.com/LINE-&-FB-Messenger-jie-he-wit-ai/) 以及 [使用 Lumen 建立你的 Facebook Messanger 聊天機器人](https://www.prgpress.com/shi-yong-Lumen-jian-li-ni-de-Facebook-Messanger-liao-tian-ji-qi-ren/) 的延伸出來，由 wit.ai 詳細的說明，給大家知道它的設定

### wit.ai 的開始

這是 wit.ai 的畫面，它需要經過一些訓練才能真正使用它的功能，現在就開始去使用它的功能吧

直接去它的網站 [wit.ai](https://wit.ai)

直接可以看到它的畫面，很簡單的告訴你它可以做到哪些部分，當然這次只有 Bot 而已

![wai.it login](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit.ai_login.png)

當你透過 Facebook 登入吧，這就是它的界面，設計層面是很簡單的畫面，進去先建立一個 app，然後就如同下方的圖片

![wai.it for me](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit.ai_for_me.png)

進入之後，就會看到它的主畫面

![wai.it](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit.ai_startup.png)

### wit.ai 從 Setting 開始做起

這裏要注意時區是 Asia/Taipei，以及語言選擇 Chinese

![wai.it](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit_ai_setting.png)


### wit.at 從 Understanding 開始訓練

一開始從 Understanding 開始，這裏假設使用者會問的文字

![wai.it](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit.ai_default.png)

因爲是用來查詢某些地方的天氣狀況，當輸入文字之後，記得要按下 Enter，否則它認爲你沒有輸入，下圖就是新竹市被當成 wit/location

![wai.it](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit.ai_test_talking.png)

下面的一樣，輸入高雄市的天氣，也是一樣的將文字直接用 wit/location

![wai.it](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/wit.ai/wit.ai_test_talking-2.png)

這裏的 location 後面會介紹如何去做判斷

### 測試輸入的文字

直接輸入：新竹市的天氣，然後就產生如下的指令
在 iTerm2 或者終端機執行下面指令，他會返回它 entities，並且會有分數還有這次的值是什麼，正確的話至少有 0.8 以上

```command
curl \
 -H 'Authorization: Bearer [Your_Key]' \
 'https://api.wit.ai/message?v=20190506&q=%E6%96%B0%E7%AB%B9%E5%B8%82%E7%9A%84%E5%A4%A9%E6%B0%A3'
{"_text":"\u65b0\u7af9\u5e02\u7684\u5929\u6c23","entities":{"location":[{"suggested":true,"confidence":0.93386,"value":"\u65b0\u7af9\u5e02","type":"value"}]},"msg_id":"1c9OcXK70BrLlbbXm"}%
```

假設你輸入的是 Test，馬上返回 entities 是空的，代表文字是不接收的，或沒有訓練到這個文字才會如此

```
curl \
 -H 'Authorization: Bearer [Your_Key]' \
 'https://api.wit.ai/message?v=20190506&q=Test'
{"_text":"Test","entities":{},"msg_id":"1LsWLw9gyQCQuxwGs"}%
``` 

然後就是程式的邏輯
1. entities 有 location 的就直接把它認爲的字詞給接過來，然後看是否與自己的 array 有一組符合就對了，譬如：新竹市的天氣，然後就會得到「**新竹市**」，而天氣以及氣溫我就靠程式解決，在拋回去給天氣的 API 就解決了
2. entities 有 greetings 的，就認爲是在問「你好、您好」之類的，然後就給它「**你好，有什麼可以協助你**」
3. entities 有 do_what 的值，馬上返回「**您好，這是聊天機器人，負責天氣預報，你可以問我「天氣如何？」、「新竹市天氣怎麼樣**」之類的話題
4. 最後什麼都沒有的話，就返回「**您好，目前並沒有此項功能，你可以問我「天氣如何？」、「新竹市天氣怎麼樣」之類的話題！**」

這樣的話，就不會給 Facebook 的審核人員認爲是不正常的訊息

### wit.ai 是簡單易懂的工具

wit.ai 我目前只用在聊天機器人，或許可以用在語音判斷，或者硬體的人機界面上可以做的更好

只不過我沒有這麼多的東西去玩，