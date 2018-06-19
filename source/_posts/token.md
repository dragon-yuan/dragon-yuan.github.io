---
title: 微信二次开发第一弹（开发者中心TOKEN配置与服务器连接）
categories:
  - Operations
date: 2015-04-22 14:19:27
---

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">本文目标：学习一种比较安全的服务器间互相验证身份的方式。  
  </pre>

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">问题：开发微信公众平台接口，开发者的服务器为了确保请求是否来自微信服务器，应该如何去做？  

</pre>

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">1)  在微信管理页面上填写URL和TOKEN，开发者服务器上也记录同样的TOKEN。  

</pre>

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">2)  微信服务器发送HTTP请求，附带上参数(注意TOKEN是不会被传输的)  

</pre>

<pre><span style="color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">参数 描述  

</span></pre>

<table style="color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;" border="1" cellspacing="0" cellpadding="4">

<tbody>

<tr>

<td style="font-size: 1em;">

<pre>signature</pre>

</td>

<td style="font-size: 1em;">

<pre>微信加密签名</pre>

</td>

</tr>

<tr>

<td style="font-size: 1em;">

<pre>timestamp</pre>

</td>

<td style="font-size: 1em;">

<pre>时间戳</pre>

</td>

</tr>

<tr>

<td style="font-size: 1em;">

<pre>nonce</pre>

</td>

<td style="font-size: 1em;">

<pre>随机数</pre>

</td>

</tr>

<tr>

<td style="font-size: 1em;">

<pre>echostr</pre>

</td>

<td style="font-size: 1em;">

<pre>随机字符串</pre>

</td>

</tr>

</tbody>

</table>

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">其中signature值通过如下摘要运算得出：</pre>

<pre style="font-size: 14px; color: #000000; line-height: 25.2000007629395px;">1\. 将token、timestamp、nonce三个参数进行字典序排序  

2\. 将三个参数字符串拼接成一个字符串进行sha1加密(这个加密是不可逆的)，并将结果的byte[]转换为16进制字符串  

</pre>

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;">3)  开发者服务器接收到signature,timestamp,nonce,echostr参数，跟服务器做同样的摘要运算，得到预期的一个signatrue，然后对比微信服务器发送过来的signature参数，如果相同，证明双方的TOKEN是一致的，开发者服务器确实接收到了来自微信服务器的请求，开发者服务器最后返回echostr，以告诉微信服务器接入成功。具体的开发者服务器校验逻辑代码如下显示。  

</pre>

* * *

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;"><span style="color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif;"><span style="font-size: 14px; line-height: 25.2000007629395px;">`<?php
/**
  * wechat php test
  */

//define your token
define("TOKEN", "xxx");
$wechatObj = new wechatCallbackapiTest();
$wechatObj->valid();

class wechatCallbackapiTest
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

		if( $tmpStr == $signature ){
			return true;
		}else{
			return false;
		}
	}
}

?>  

`</span></span></pre>

* * *

<pre style="margin: 0px; padding: 0px; color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px;"><span style="color: #000000; font-family: Helvetica, Tahoma, Arial, sans-serif;"><span style="font-size: 14px; line-height: 25.2000007629395px;">`[公众平台开发接口介绍](http://mp.weixin.qq.com/wiki/home/index.html "公众平台开发接口介绍")`  
</span></span></pre>
