---
layout: post
title: "Google reCAPTCHA v3 的用法"
author: patrick
categories: [Google]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google_v3/reCAPTCHA_v3_1.png"  
tag: featured
---

一般設計使用者登入的驗證碼，不外乎是填寫英文數字與後端的 SESSION 是否符合，如果是符合就可以登入，而驗證碼上面可以加上一些干擾圖案之類的，爲的就是防止機器人登入。

reCAPTCHA v3 的版本與過往 reCAPTCHA v2 最大的不同點，在於網站使用者不再需要透過圖型驗證碼或打勾確認你是否真人，而是在網站後段自動紀錄使用者在網站中瀏覽的行為過程，假設有類似在連絡表單中不斷提交重複文字之類的行為時，將會將其判定為機器人。

所以 reCAPTCHA v3 是判斷你的分數，它是有 0.1 ~ 1.0 之間分數，不過建議是方式大於 0.5 以上才算是一般人，這個方式是由 Google 的方式，不能由開發者可以干擾，所以它有一定的資料量讓你可以判斷才行。

之前介紹過 [Google reCAPTCHA「我不是機器人」爲網站添加安全驗證機制](https://www.prgpress.com/Google-reCAPTCHA-wo-bu-shi-ji-qi-ren-wei-wang-zhan-tian-jia-an-quan-yan-zheng-ji-zhi/)，這次來介紹 v3 的使用方法 

### reCAPTCHA v3 的使用方法

看過之前的 reCAPTCHA v2 所以就不再介紹它的申請

這次是 v3 爲主，跟之前一樣，有個網站金鑰以及密鑰

![reCAPTCHA v3](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google_v3/google_v3_validate.png)

先給登入網站載入 api.js

```
<script src="https://www.google.com/recaptcha/api.js?render=[你的網站金鑰]"></script>
```

然後看登入頁面，應該有 reCAPTACHA 的圖案在右下角出現

 ![reCAPTCHA v3](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google_v3/reCAPTCHA_v3.png)
 
然後送出去給網站驗證，驗證的部分改一下

```
$captcha = $_POST['recaptcha_response'];
$secretKey = '複製前面的密鑰';

$url = 'https://www.google.com/recaptcha/api/siteverify?secret=' . urlencode($secretKey) . '&response=' . urlencode($captcha);
$response = file_get_contents($url);
$responseKeys = json_decode($response, true);

if ($responseKeys['score'] >= 0.5) {
   // success
} else {
   // failure
}
```

主要是 score 的分數，只要是 >= 5.0 以上，就算真人了

這樣是不是更簡單了

### 如何知道 Google reCAPTCHA v3 在正常運作？

直接看後端就可以知道它有沒有實際的運作，以底下的圖來看就可以看出左邊是實際有多少人使用它，以及圖案顯示 7 天的使用狀況

在它的右邊是平均達到多少分數，以及它的人次，表示所有人都是 0.9 的分數，所以全部屬於真人在登入

因爲裏面沒有可疑的流量，所以沒有可以看出來這部分的流量

![google_recaptcha_v3](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/google_v3/google_recaptcha_v3.png)

只是它依然是要有點防護，譬如 SESSION['google_code'] 記住某個值，只要與前端不符合的就直接讓它退出
這樣至少先讓自己的 server 過濾，而不是只有單純靠它的 server 爲主

### 驗證碼是要使用 v2 還是 v3 ？

reCAPTCHA v3 是一項全新的技術，不排除 v3 的方法，但是絕大部分的人而言 reCAPTCHA v2 還是網站保護的首選，它還是看得到保護的機制是看得到的，對網站運作而言也比較穩定，如果有任何關於 reCAPTCHA 網站驗證方面的問題，也歡迎在下方留言討論吧！