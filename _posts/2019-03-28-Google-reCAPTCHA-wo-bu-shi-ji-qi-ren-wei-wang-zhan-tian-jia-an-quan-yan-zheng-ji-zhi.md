---
layout: post
title: "Google reCAPTCHA「我不是機器人」爲網站添加安全驗證機制"
author: patrick
categories: [Mac, Macbook]
image: "https://www.google.com/recaptcha/intro/images/hero-recaptcha-invisible.gif"  
---

Google reCAPTCHA 的做法，是由 Google 提供的方法來決定你是否爲機器人，所以可以用在註冊、登入甚至於聯絡我們的表單等等，Google reCAPTCHA 申請的做法很覺得，不過它要的是網域 ( Domain Name )，不能使用 IP，在這裏就教你如何去做 

## 網址

它的網址：https://www.google.com/recaptcha/intro/v3.html

進入之後，從右邊的「Admin console」立刻進入頁面

![reCAPTCHA__Easy_on_Humans__Hard_on_Bots](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google/reCAPTCHA__Easy_on_Humans__Hard_on_Bots.png)

## 新增頁面

然後就如圖所示，右邊的 + 來新增頁面

![reCAPTCHA](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google/reCAPTCHA.png)

照着下圖填完，記得要按下接受打勾，以及確定，後面有金鑰，就完成申請了

![reCAPTCHA_1](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google/reCAPTCHA_3.png)

![reCAPTCHA_2](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google/reCAPTCHA_2.png)

到這裏就完成了 Google reCAPTCHA 的資料

大概有人會問，爲什麼不使用 v3 的功能，因爲 v3 的驗證是看不到，主要是它的伺服器會加以判斷，實際會返回分數，所以還是 v2 比較好一些

## 開始就是自己寫程式

這段代碼直接貼在網頁上

```html
貼在 <head> 的後面

<script src="https://www.google.com/recaptcha/api.js"></script>
```

第二個是貼到要顯示的位置
```html
<div class="g-recaptcha" data-sitekey="這裏直接貼上網站金鑰"></div>
```

到這裏差不多就完成了

![reCAPTCHA_2](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google/Cursor_和_Google_reCAPTCHA我不是機器人，為註冊表單或論壇網站添加安全驗證機制。___Techmarks劃重點.png)

## 驗證它的我不是機器人

這個就簡單多了，只要複製就可以了，主要是 Google SiteVerify 做了驗證

```php
$captcha = $_POST['g-recaptcha-response'];
$secretKey = "前面的密鑰";
$ip = $_SERVER['REMOTE_ADDR'];

$url = 'https://www.google.com/recaptcha/api/siteverify?secret=' . urlencode($secretKey) .  '&response=' . urlencode($captcha);
$response = file_get_contents($url);
$responseKeys = json_decode($response,true);

if($responseKeys["success"]) {
    // success
} else {
    // error
}
```

以上是 Google reCAPTCHA 的做法