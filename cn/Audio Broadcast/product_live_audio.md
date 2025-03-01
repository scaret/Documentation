
---
title: 产品概述
description: 
platform: All Platforms
updatedAt: Mon May 27 2019 10:16:14 GMT+0800 (CST)
---
# 产品概述
Agora 音频互动直播（Audio Broadcasting）可以实现一对多，多对多的纯音频互动直播。

Agora 音频互动直播和 [Agora 语音通话](https://docs.agora.io/cn/Voice/product_voice?platform=All%20Platforms)的区别是：
- 语音通话，不区分主播和观众，所有用户都可发言，默认流畅和低延时优先，典型场景如多人语音会议。
- 语音直播，用户分为主播和观众，只有主播可以自由发言，默认高音质优先，典型场景如在线音乐直播。

常见的 CDN 直播是一个主播和多个观众，是单向的。而互动直播还能多个主播之间，观众与主播之间连麦，就像在小剧场里观众可以上台表演一样。适用于娱乐直播如狼人杀、教育直播如小班课、电商直播中的导购问答等强互动场景。



## 功能和场景

Agora 音频互动直播提供丰富的功能，你可以根据自己的场景需求灵活组合。

| 主要功能             | 功能描述                                                     | 典型适用场景                                                 |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 客户端连麦           | 观众与主播连麦聊天，观众围观。                               | <li>大型直播时，主播邀请观众互动 <li>狼人杀、剧本杀          |
| 跨直播间连麦         | 多个主播跨直播间，连麦互动，观众围观。                       | PK 连麦                                                      |
| 伴奏混音             | 将本地或在线的音频和用户声音，同时发送并播放给频道内其他用户 | <li>在线合唱 <li>针对幼儿的音乐互动课堂                      |
| 变声和混响        | 提供多种预置的变声和混响效果，同时支持灵活调整用户声音的音调、均衡及混响效果。 | <li>一起 KTV<li>语音聊天室变声 |
| 听声辨位          | 设置远端用户声音出现的位置，增加游戏角色的方位感，还原真实游戏场景。 | 吃鸡游戏                       |
| 修改音频原始数据   | 可支持变声，支持获取媒体引擎的原始语音数据，对原始数据进行处理 | <li>语音聊天室变声                           |
| 在线媒体流输入       | 可以将媒体流作为一个发送端接入正在进行的直播房间。通过将正在播放的音频添加到直播中，主播和观众可以在一起收听/观看媒体流的同时，实时互动。 可以对输入源的属性进行设置。 | <li>主播和观众一起听演唱会      |
| 推流到 CDN           | 将频道内的音频内容通过 CDN 推送到其他 RTMP 服务器： <li>能够随时启动或停止推流 <li>能够在不间断推流的同时增减推流地址 | <li>在朋友圈、微博等推广直播内容<li>频道人数超限时，让更多人参与直播 |

更多的玩法，点击查看示例代码：

- [PK 连麦](https://github.com/AgoraIO/ARD-Agora-Online-PK/blob/master/README.zh.md)
- [一起 KTV](https://github.com/AgoraIO/Agora-Online-KTV/blob/master/README.zh.md)
- [在线语音聊天室](https://github.com/AgoraIO-Usecase/Chatroom)
- [剧本杀](https://github.com/AgoraIO-Usecase/Murder-Mystery-Game)

## 关键特性

| 特性                      | Agora 互动直播指标                                           |
| ------------------------- | ------------------------------------------------------------ |
| SDK 包体积                | 3.69 M - 7.75 M                                              |
| 多主播互动                | 17 人                                                        |
| 最多观众人数              | 100 万                                                       |
| 跨频道主播连麦            | 支持                                                         |
| 音频属性                  | <li>音频采样率：16 KHz - 48 KHz <li>支持单、双声道           |
| 音频抗丢包率              | 上下行抗丢包率 70%                                           |

### 平台兼容

音频互动直播支持 iOS、Android、Windows、macOS、Linux、Web、小程序，并支持平台间互通，具体的兼容性要求见下表。

| 平台       | 支持版本                                                     |
| ---------- | ------------------------------------------------------------ |
	| Android    | <p>4.1+</p><p>Android SDK 支持如下架构：</p><ul><li>ARMv7<li>ARM64<li>X86                                                         |
| iOS        | 8.0+                                                         |
| Windows    | XP SP3+                                                      |
| macOS      | 10.0+                                                        |
| 微信小程序 | 支持                                                         |
| Web        | <li>Chrome 58+ <li>Chrome 49（仅 Windows XP）<li>Firefox 56+ <li>Safari 11+ <li>Opera 45+ <li>QQ 10+ <li>360 安全浏览器 9.1+ |

## Demo 体验

### 音频互动直播 - Agora Live

在应用市场下载 Agora Live app，快速体验超低延迟多人连麦互动直播。

- [Android](http://android.myapp.com/myapp/detail.htm?apkName=io.agora.vlive)
- [iOS](https://itunes.apple.com/cn/app/id1116886856?mt=8)
- [Web](https://webdemo.agora.io/videocall/?_ga=2.212778772.1474390666.1541382528-1513744824.1530171825)
- [Windows](http://download.agora.io/avc/AgoraLiveBroadcast_for_windows_2.2.0.zip?_ga=2.231750175.1098053192.1540804434-1796221125.1530266296)

### 语音聊天室 - 分贝

在应用市场下载分贝 app，快速体验多人语音聊天室，感受麦序麦位、听歌、聊天等玩法。

- [iOS](https://itunes.apple.com/cn/app/id1417827292?mt=8)
