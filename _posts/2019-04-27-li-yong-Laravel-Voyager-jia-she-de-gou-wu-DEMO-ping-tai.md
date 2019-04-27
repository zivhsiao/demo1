---
layout: post
title: "利用 Laravel + Voyager 架設的購物 DEMO 平臺"
author: patrick
categories: [Heroku]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/heroku/截圖_2019-04-13_上午9.46.47.png"  
---

利用 Laravel 以及 Voyager 來架設的購物 DEMO 平臺，因爲 Laravel 的部分是 Andre Madarang 寫出來的，所以暫時保留原先的樣子

## 開始用 git clone 下來吧

原始來源：https://github.com/drehimself/laravel-ecommerce-example

改版的來源：https://github.com/zivhsiao/ecommerce-example.git

爲什麼採取別人的 git 再 fork 給自己

因爲學習別人的做法，才能讓自己更加精進，來彌補自己所沒有辦法的部分，才會找個比較快速的方法

它是使用 Stripe，目前是有支援臺灣的部分，它的幣別是 TWD
只是 Stripe 不行在臺灣開戶，最近的是香港，我們用它在於測試用並且檢查卡號是否正常

他會依照當下的匯率來換算 USD，所以在它的測試數據中只有 USD

#### 這是測試卡號
| 卡號 | 月/年 CVC | 說明 |
| --- | --- | --- |
| 4242 4242 4242 4242 | 04/24 242 | Visa |
| 4000 0000 0000 0069 | 04/24 242 | 過期卡測試 |


## 準備讓網站動起來

先把它 git clone 下來一份，然後照着指令一步一步往下做

```
git clone https://github.com/zivhsiao/ecommerce-example.git
```

![git clone](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/git_clone.png)

再來就是 composer install

```
composer install
```

![composer install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/composer_install.png)


跑完的話，要先吧 .env 給複製一份，然後繼續


```
cp .env.example .env

php artisan key:generate
```


然後修改 .env，這裏有幾個地方需要注意

```
# 這一定要設立
APP_URL=http://ecommerce-example.localhost:8888

# 因爲我採取 MAMP 去架設起來
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=8889
DB_DATABASE=demo_ecommerce
DB_USERNAME=root
DB_PASSWORD=hezrid5
DB_SOCKET=/Applications/MAMP/tmp/mysql/mysql.sock

# mail 的部分是採取 mailtrap，只有我自己看得到
MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_FROM_ADDRESS=service@localhost
MAIL_FROM_NAME=Service
MAIL_ENCRYPTION=tls

# Stripe 的 api, secret，現在只能用測試
STRIPE_KEY=pk_test_xxxxxxxxxxxxxxx
STRIPE_SECRET=sk_test_xxxxxxxxxxxxxxx

# Algolia 這個可以不要，有的話更好
ALGOLIA_APP_ID=G0xxxxxx
ALGOLIA_SECRET=76xxxxxxxxxxxxxxxx
```

如果到這裏的話，沒有問題就下指令吧，這是它封裝的 ecommerce 直接 install，如果有 mysql 的問題，就回過頭來檢查看看，然後再重新執行

```
php artisan ecommerce:install
```

![composer install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/php_artisan_ecommerce_install.png)

## 然後修改程式吧！

因爲它的程式預設幣別是 USD，有一些地方要做修改

修改幣別的程式
- app/helpers.php
- app/Product.php

```php
//第一個
//直接找出來
return money_format('$%i', $price / 100);
//用來置換
return "TWD " . number_format($price );

//第二個
//直接找出來
return money_format('$%i', $this->price / 100);
//用來置換
return "TWD " . number_format($this->price );
```

然後去修改 config/cart.php
```php
'tax' => 5, // 因爲是臺灣，只有 5% 的稅

'format' => [
    'decimals' => 0, //小數點後面幾位數字，目前是改爲 0
    'decimal_point' => '', //小數點的區分符號，目前是空白 
    'thousand_seperator' => ''
],
```

接下來是結賬完成的通知信
- resources/view/emails/order/placed.blade.php

```php
**Order Total:** TWD {{ round($order->billing_total) }}

Price: TWD {{ round($product->price)}} <br>
```

然後測試看看，理論上是沒有問題的了

![composer install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/web_index_01.png)

![composer install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/web_index_022.png)

![composer install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/web_index_03.png)

#### 這裏有我的操作模式

![composer install](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/laravel_ecommerce/Laravel_Ecommerce_Backbeat_Go_810.gif)


這樣在結賬的畫面就很正常了，完全符合臺灣的口味了