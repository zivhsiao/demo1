---
layout: post
title: "微信公衆平臺後開發界面的 URL 和 Token 如何驗證？"
author: patrick
categories: [PHP 工程師的日常]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/daily/wechat_01.png"  
---

在臺灣要如何成爲微信的開發者，首先必須要有公司才行，還要有臺灣居民來往大陸通行證，第二就必須要有大陸在地的企業去申請，否則申請是沒有用的

我接觸微信，剛好都是公司的關係，所以還是要公司給你玩玩

### 準備微信的後臺

現在要成為微信開者的教學如下


### PHP 的程式

官網的測試：http://mp.weixin.qq.com/mpres/htmledition/res/wx_sample.zip

這是 test 的程式，這樣就好了

```
<?php

//define your token
define("TOKEN", "你的伺服器提供的 Token");
$wechatObj = new wechatCallbackapi();
$wechatObj->valid();

class wechatCallbackapi
{
	public function valid()
    {
        $echoStr = $_GET["echostr"];

        //valid signature , option
        if($this->checkSignature()){
        	echo $echoStr;
        	exit;
        }
    }

    public function responseMsg()
    {
		//get post data, May be due to the different environments
		$postStr = $GLOBALS["HTTP_RAW_POST_DATA"];

      	//extract post data
		if (!empty($postStr)){
                
              	$postObj = simplexml_load_string($postStr, 'SimpleXMLElement', LIBXML_NOCDATA);
                $fromUsername = $postObj->FromUserName;
                $toUsername = $postObj->ToUserName;
                $keyword = trim($postObj->Content);
                $time = time();
                $textTpl = "<xml>
							<ToUserName><![CDATA[%s]]></ToUserName>
							<FromUserName><![CDATA[%s]]></FromUserName>
							<CreateTime>%s</CreateTime>
							<MsgType><![CDATA[%s]]></MsgType>
							<Content><![CDATA[%s]]></Content>
							<FuncFlag>0</FuncFlag>
							</xml>";             
				if(!empty( $keyword ))
                {
              		$msgType = "text";
                	$contentStr = "Welcome to wechat world!";
                	$resultStr = sprintf($textTpl, $fromUsername, $toUsername, $time, $msgType, $contentStr);
                	echo $resultStr;
                }else{
                	echo "Input something...";
                }

        }else {
        	echo "";
        	exit;
        }
    }
		
	private function checkSignature()
	{
        $signature = $_GET["signature"];
        $timestamp = $_GET["timestamp"];
        $nonce = $_GET["nonce"];	
        		
		$token = TOKEN;
		$tmpArr = array($token, $timestamp, $nonce);
		sort($tmpArr);
		$tmpStr = implode( $tmpArr );
		$tmpStr = sha1( $tmpStr );
		
		if( $tmpStr === $signature ){
			return true;
		}else{
			return false;
		}
	}
}

?>
```

#### 登錄 https://mp.weixin.qq.com 

然後在公眾平台後台管理頁面 –> 開發者中心頁，點擊「修改配置」按鈕，填寫 URL、Token 和 EncodingAESKey

記得要填入網址，如：https://test.demo.com，然後它的 Token 是你隨便打出來的，EncodingAESKey 是隨機生成

消息加密方式：選擇明文模式，點擊提交 這裏如果第一次沒有成功可以多點幾次，這是由於你的服務器延時造成的

記得上面的 TOKEN 要修改成爲你的值就可以了，如果有錯誤的話就檢查一下是否都是沒有問題


