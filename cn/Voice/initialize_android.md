
---
title: 创建实例
description: 安卓平台初始化引擎
platform: Android
updatedAt: Thu Dec 06 2018 08:42:16 GMT+0800 (CST)
---
# 创建实例
在创建实例前，请确保你已完成环境准备、安装包获取等步骤，详见[集成客户端](../../cn/Voice/android_audio.md)。
## 实现方法

导入以下 Agora API 包:

- `io.agora.rtc.Constants`
- `io.agora.rtc.IRtcEngineEventHandler`
- `io.agora.rtc.RtcEngine`
- `io.agora.rtc.video.VideoCanvas`

进入频道之前，调用 `create` 创建一个实例。在该方法中:

- 填入获取到的 App ID。只有 App ID 相同的应用程序才能进入同一个频道进行互通。
- 指定一个事件回调。SDK 通过指定的事件通知应用程序 SDK 的运行事件，如: 加入或离开频道，新用户加入频道等。

```java
import io.agora.rtc.Constants;
import io.agora.rtc.IRtcEngineEventHandler;
import io.agora.rtc.RtcEngine;
import io.agora.rtc.video.VideoCanvas;

...

private void initializeAgoraEngine() {
    try {
        mRtcEngine = RtcEngine.create(getBaseContext(), getString(R.string.agora_app_id), mRtcEventHandler);
    } catch (Exception e) {
        Log.e(LOG_TAG, Log.getStackTraceString(e));

        throw new RuntimeException("NEED TO check rtc sdk init fatal error\n" + Log.getStackTraceString(e));
    }
}
```

> 请确保在调用其他方法前先调用 `create` 方法创建并初始化 RtcEngine。

## 相关文档
完成创建实例后，你可以使用 Agora SDK，依次实现如下功能进行语音通话：
* [加入频道](../../cn/Voice/join_communication_android.md)
* [发布和订阅音频流](../../cn/Voice/publish_android_audio.md)

如果对网络或音质有特殊的需求，你还可以在加入频道前：
* [进行通话前网络质量检测](../../cn/Voice/lastmile_android.md)
* [使用双声道/高音质](../../cn/Voice/audio_profile_android_audio.md)


