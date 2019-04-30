---
layout: post
title: "Voyager 的介紹以及使用 (一)"
author: patrick
categories: [Laravel]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/laravel-voyager.jpeg"  
tag: featured
---

專門介紹 Voyager 是做什麼的，以及使用它的方法

### Voyager 是什麼？

Voyager 是一個管理界面，可以很輕易的為你的 app 建構 CRUD 功能，建構不同的選單，以及管理多媒體檔案。

在管理介面的 Database 裏面可以直接用來管理資料庫及資料表，BREAD (Browse, Read, Edit, Add, Delete) 功能則是可以很用非常便利的方式，直接設定資料表欄位可以出現在在瀏覽、編輯、添加、刪除或者全部都看到的，全部都可以設定，尤其他的功能屬性是什麼，可以是文字欄位、選單、圖片、檔案、等，除了這些，還有可選細項 ( Additional Field Options ) 可以處理，這裏蠻方便的。

### Voyager 可以用在哪裏？

不論是 CMS、Blog 乃至於購物平臺，都可以使用它節省了許多的力氣，正常下只要建立起來，基本 CMS、Blog 就已經好了一大半，只要注意前臺就可以了。

基本是透過後臺界面，將所有的東西都寫入資料庫，所以它是全部由資料庫建立起來，舉凡 Products、Orders 等等。

主要是 Laravel 搭配 Voyager 可以做網站就無往不利了。

### BREAD 的可選細項 ( Additional Field Options ) 的說明

直接看這裏，可以複製套用就可以了
- 網站說明：[https://voyager.readme.io/docs/additional-field-options](https://voyager.readme.io/docs/additional-field-options)

### 基本的安裝流程

Laravel 這部分要先安裝

```
composer create-project  --prefer-dist laravel/laravel .
```

然後直接安裝 Voyager，這裏還沒有安裝完成

```
composer require tcg/voyager
```

### 設定資料庫

因爲我使用 Macbook，所以這裏採用 MAMP Pro 來當作開發環境

這是 MAMP Pro 的畫面 

![MAMP Pro](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/MAMP_Pro.png)

底下是要改的地方，確定一定可以連得到就好

```
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=8889
DB_DATABASE=blog1
DB_USERNAME=root
DB_PASSWORD=hezrid5
DB_SOCKET=/Applications/MAMP/tmp/mysql/mysql.sock
```

### 然後就安裝 voyager 

如果需要 dummy 的資料，就直接用 --with-dummy 

其實覺得它裏面還有需要學習的，就使用 dummy 就好 

```
php artisan voyager:install --with-dummy
```

等他跑完就可以了

![voyager install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/Voyager_install.png)

這裏就可以看到它的畫面，它已經幫你把基本的都架好了

![voyager login](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/Voyager_login.png)

因爲用 dummy 產生的資料，所以用帳號密碼就可以登入了

登入之後，記得要從 users 增加一個帳號來處理

```
email: admin@admin.com
password: password
```

登入畫面如下圖所示

![voyager admin screen](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/voyager_admin.png)

### 開始寫 Blog

畫面基本是用 Posts 爲主

![voyager admin screen](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/voyager_posts.png)

預設有 4 則 posts

![voyager admin screen](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/posts_article.png)

看我的 Posts 的操作吧

![voyager admin screen](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/voyager/my_post.gif)

基本已經完成了後端的程式了，基本連程式都沒有碰到就完成了 Blog 的管理，後面的部分是前臺的畫面，因爲是 Blog，所以只有文章列表、文章內頁，照着步驟試着做看看吧！

