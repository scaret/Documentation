
---
title: 加入频道
description: windows平台加入频道
platform: Windows
updatedAt: Thu Dec 13 2018 08:10:27 GMT+0800 (CST)
---
# 加入频道
在加入频道前，请确保你已完成环境准备、安装包获取等步骤，详见[客户端集成](../../cn/Interactive%20Broadcast/windows_video.md)。

## 实现方法
App 在加入频道前，需要先设置频道模式，再加入频道。

### 设置频道模式为直播
初始化实例后，调用 <code>setChannelProfile</code> 方法设置频道模式。SDK 会根据所设置的频道模式使用不同的优化手段。

在该方法中，将频道模式设置为直播模式。直播模式适用于互动直播场景。频道内有主播和观众两种角色，主播收发音视频消息，观众只收不发。
 
> - 该方法必须在加入频道前调用才能生效。
> - 同一频道只能设置一种频道模式。如果需要切换频道模式，请先调用 `destroy` 方法销毁后重新创建一个 Engine 实例，再调用该方法将频道设置为其他模式。


```
nRet = m_lpAgoraEngine->setChannelProfile(CHANNEL_PROFILE_LIVE_BROADCASTING);
```

### 加入直播频道
调用 <code>joinChannel</code> 方法加入频道。

在该方法中：

-   传入能标识用户角色和权限的 Token。Token 需要在你的服务器端生成，详细生成办法见[密钥说明](../../cn/Audio%20Broadcast/token.md)。

	> 在 [Dashboard](https://dashboard.agora.io/) 注册项目后，你可以获取一个临时 Token 用于测试。生产环境下，我们推荐你使用在自己的服务端生成的正式 Token。
-   传入能标识频道的频道 ID。输入相同频道 ID 的用户会进入同一个频道。
-   传入能标识用户身份的用户 UID。请确保频道内每个用户的 UID 必须是独一无二的。

> 如果已在通话中，则必须调用 <code>leaveChannel</code> 方法退出当前通话，才能进入下一个频道。

```
LPCSTR lpStreamInfo = "{\"owner\":true,\"width\":640,\"height\":480,\"bitrate\":500}";
nRet = m_lpAgoraEngine->joinChannel(lpToken, lpChannelName, lpStreamInfo, nUID);
```


## 相关文档

成功加入频道后，你可以使用 Agora SDK，实现如下功能进行互动直播：

- [切换用户角色](../../cn/Interactive%20Broadcast/role_windows.md)
- [发布和订阅音视频流](../../cn/Interactive%20Broadcast/publish_windows_live.md)

在直播过程中，如果对音量、音效、视频分辨率等有特殊需求，你还可以：

- [调整通话音量](../../cn/Interactive%20Broadcast/volume_windows.md)
- [播放音效/音乐混音](../../cn/Interactive%20Broadcast/effect_mixing_windows.md)
- [调整音调、音色](../../cn/Interactive%20Broadcast/voice_effect_windows.md)
- [设置视频属性](../../cn/Interactive%20Broadcast/videoProfile_windows.md)
