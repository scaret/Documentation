
---
title: 创建并初始化 Client 对象
description: Web SDK 初始化客户端对象
platform: Web
updatedAt: Mon Mar 25 2019 09:35:37 GMT+0800 (CST)
---
# 创建并初始化 Client 对象
在创建并初始化 Client 对象前，请确保你已完成环境准备、安装包获取等步骤，详见[集成客户端](../../cn/Voice/web_prepare.md)。

## 实现方法
### 创建 Client 对象
用 `AgoraRTC.createClient` 方法创建 Client 对象，设置 `mode` 和 `codec` 。

```javascript
var client = AgoraRTC.createClient({mode: 'live', codec: "h264"});
```

### 初始化 Client 对象
创建 Client 对象后，将项目的 App ID 填入 `client.init` 方法，即可初始化 Client。

```javascript
client.init(<APPID>, function () {
  console.log("AgoraRTC client initialized");

}, function (err) {
  console.log("AgoraRTC client init failed", err);
});
```

> 请确保在调用其他 API 前先调用 `create` 和 `client.init` 方法创建并初始化 AgoraRtcEngine。

## 相关文档
初始化 Client 对象后，你可以使用 Agora SDK，依次实现如下功能进行通话/直播：
- [加入频道](../../cn/Voice/join_web_audio.md)
- [发布和订阅音频流](../../cn/Voice/publish_web_audio.md)

如果对网络或音质有特殊的需求，你还可以在加入频道前：
- [使用双声道/高音质](../../cn/Voice/audio_profile_web.md)

