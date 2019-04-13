---
layout: post
title: "Heroku 的 Laravel 範例"
author: patrick
categories: [Heroku]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午9.46.47.png"  
---

Heroku 是一個支持多種編程語言的 PaaS (Platform-as-a-Service)。早在 2010 年就已經被 Salesforce 收購了。Heroku 作為最開始的雲平台之一，從 2007 年 6 月起開始開發，當時它僅支持 Ruby，後來增加了對 Java、Node.js、Scala、Clojure、Pytho、PHP 和 Perl 的支持。

因爲我是 Laravel 的支持者，所以只有 PHP 爲主要的選擇。

### 爲何選用 Heroku

Heroku 的部署流程異常簡單。只需要將源碼加入到 Git 中即可，其它額外操作 Heroku 都會幫你自動處理好。

#### Heroku 註冊並且登入

![Heroku 註冊畫面](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午9.46.28.png)

完成註冊之後，直接安裝它的 CLI，按照 [這裏的說明](https://devcenter.heroku.com/articles/heroku-cli) 就可以了

之後要按下 New 的按鈕

![](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午9.47.23.png)

給你的專案一個名稱吧，不能有重複的名稱

![](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午9.48.05.png)

然後到 windows 的「命令提示字元」或 Mac 的「終端機」

直接輸入以下的指令

```
heroku login
```

![Heroku 登入的畫面](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午9.50.16.png)


#### 這部分要懂得 git 的運作

因爲是 Laravel，當大家懂得 composer 的做法

所以直接建立它的專案，這是全新的 Laravel 的做法，必須要再 git init 之前就一定先建立起來，否則會建立不起來

```
composer create-project  --prefer-dist laravel/laravel .
```

![composer 運行的畫面](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午11.58.59.png)

當他跑完了，就執行下面的指令，project name 就代表你所建立的名稱

```
git init
heroku git:remote -a [project name]
```


#### 產生一個 Procfile 的檔案

要讓 web 修改爲以 /public 目錄爲主，所以必須產生一個 Procfile 的檔案
``` 
echo "web: vendor/bin/heroku-php-apache2 public/" > Procfile
```

然後執行以下的命令

```
git add .
git commit -am "make it better"
git push heroku master
```

**注意：他是要 push 的時候才會針對裏面檔案去做處理並且執行起來，如果裏面有錯誤，代表你的程式有些許問題，然後就不會跑成功**

大功告成，然後去執行你的 web

![Laravel 成功的畫面](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_下午12.06.05.png)

整個過程覺得很簡單吧！

在下一篇就直接用 Voyager 來管理系統，我就以 Blog 開始吧

