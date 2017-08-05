---
title: 阿里云直播配置与使用（初体验）
categories:
  - Operations
date: 2017-08-03 23:09:27
---
完整的推流地址：
形如：rtmp://video-center.alivecdn.com/{AppName}/{StreamName}?vhost={yourdomain}
```js
// 说明 video-center.alivecdn.com是直播中心服务器，允许自定义
// 例如您的域名是your.example.com（注意：该域名不可以和你的直播加速域名相同）
// 可以设置DNS，将您的 域名CNAME指向video-center.alivecdn.com即可 
// app-name是应用名称，支持自定义，可以更改video-name是流名称，支持自定义
// 可以更改 vhost参数是最终在边缘节点播放的域名，即你的直播加速域名。
```

推流（OBS）：
例如：rtmp://video.dragon-yuan.me/live_dragon/dragon?vhost=live.dragon-yuan.me
推流则需要配置如下：
```js
// FMS(URL) 为 rtmp://video.dragon-yuan.me/live_dragon/
// 串流码 为 dragon?vhost=live.dragon-yuan.me
```

鉴权计算：
```js
rtmp://video-center.alivecdn.com/{AppName}/{StreamName}?
vhost={yourdomain}&auth_key={timestamp}-{rand}-{uid}-{hashvalue}
```
字段描述
```html
timestamp：失效时间=时间戳+有效时间，CDN服务器拿到请求后，首先会判断请求中的失效时间是否小于当前时间，
如果小于，则认为过期失效并返回HTTP 403错误。

rand：随机数，一般设成0

uid：暂未使用（设置成0)

hashvalue：通过md5加密算法计算出的32位验证串
```

推流则需要配置如下：
```js
// FMS(URL) 为 rtmp://video.dragon-yuan.me/live_dragon/
// 串流码 为 dragon?vhost=live.dragon-yuan.me&auth_key=.................
```

收看地址为：
```html
http://live.dragon-yuan.me/live_dragon/dragon.flv?auth_key=.................
```