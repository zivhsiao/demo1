---
layout: post
title: "Heroku 裏面的 PHP 7.3 安裝額外的 Extension"
author: patrick
categories: [Heroku]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/Heroku_logo.svg.png"  
---

Heroku 是一個支援多種程式語言的雲平台即服務。在 2010 年被 Salesforce.com 收購。Heroku 作為最開始的雲平台之一，從 2007 年 6 月起開發，當時它僅支援 Ruby，但後來增加了對 Java、Node.js、Scala、Clojure、Python 以及 PHP 和 Perl 的支援。基礎作業系統是 Debian，在最新的堆疊則是基於 Debian 的 Ubuntu。 

這是針對 Heroku 的說明

Heroku 免費使用是有限制，它的限制是必需要運行 30 分鐘，就要睡眠一次，不過可以透過 [UPTimeRobot](https://uptimerobot.com) 去解決，不過時間是 500hr，只有信用卡註冊可以 1000hr，如果要用到 2 台 server 就可能會用光光，這一點需要注意。

### Heroku 的 PHP 額外安裝 Extension

首先要先產生 composer.json，然後它會產生 composer.lock

```
composer init
```

打開 composer.json，將需要的填入，因爲我寫的有 gd, exif, mbstring 都有用到，所以在 composer.json 寫進去


```json
{
    "require": {
        "ext-exif": "*",
        "ext-gd": "*",
        "ext-mbstring": "*"
    }
}
```

如果不清楚的話，就到這裏去看看有沒有額外的安裝

[Heroku PHP Support](https://devcenter.heroku.com/articles/php-support)

最後 composer update 就完成了 