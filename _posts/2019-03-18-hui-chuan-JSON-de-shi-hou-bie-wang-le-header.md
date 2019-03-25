---
layout: post
title: "回傳 JSON 的時候，別忘了 header"
author: patrick
categories: [PHP]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/php/php-logo-272x204.png"  
---

回傳 JSON 的時後, 常常忘了送出 header，而導致頁面整個失敗


只要回傳 JSON 的格式，就要給 header


```php
header('Content-Type: application/json; charset=utf-8');
```

寫出來這是怕忘記

JSON 是用純文字的 Type 回傳，只是它是 JSON 格式，然後給它 utf8，這樣就沒有問題啦 XD
