
---
title: 设置视频属性
description: 
platform: macOS
updatedAt: Thu May 30 2019 07:49:39 GMT+0800 (CST)
---
# 设置视频属性
## 功能简介
在视频通话或互动直播中设置视频属性，可以根据用户喜好，调整视频画面的清晰度和流畅度，获得较高的用户体验。

视频属性一般包含视频分辨率、帧率、码率、方向模式等数据。

## 实现方法

在设置视频属性前，请确保你已完成环境准备、安装包获取等步骤，详见[集成客户端](../../cn/Video/mac_video.md)。

Agora SDK 通过 `setVideoEncoderConfiguration` 方法来设置视频相关的属性，比如分辨率、码率、帧率等。参数均为理想情况下的最大值。当视频引擎因网络环境等原因无法达到设置的分辨率、帧率或码率的最大值时，会取最接近最大值的那个值。

我们建议根据[视频属性参考表](#video_profile)设置该方法中各参数的值。

```swift
// swift
// 配置一个 VideoEncoderConfiguration 实例，参数可参考下文中的 API 参考链接
let config = AgoraVideoEncoderConfiguration(size: size, frameRate: frameRate, bitrate: bitrate, orientationMode: orientationMode, degradationPreference: degradationPreference)

agoraKit.setVideoEncoderConfiguration(config)
```

```objective-c
// objective-c
// 配置一个 VideoEncoderConfiguration 实例，参数可参考下文中的 API 参考链接
AgoraVideoEncoderConfiguration *config = [[AgoraVideoEncoderConfiguration alloc] initWithSize: size frameRate: frameRate bitrate: bitrate orientationMode: AgoraVideoOutputOrientationModeAdaptative degradationPreference: AgoraDegradationMaintainQuality];

[agoraKit setVideoEncoderConfiguration: config];
```

<a id="video_profile"></a>
### 视频属性参考表

| 分辨率<br>(宽 x 高) | 帧率<br>(fps) | 基准帧率<br>(Kbps，适用于通信) | 直播帧率<br>(Kbps，适用于直播) |
| ------------------- | ------------- | ------------------------------ | ------------------------------ |
| 160 x 120           | 15            | 65                             | 130                            |
| 120 x 120           | 15            | 50                             | 100                            |
| 320 x 180           | 15            | 140                            | 280                            |
| 180 x 180           | 15            | 100                            | 200                            |
| 240 x 180           | 15            | 120                            | 240                            |
| 320 x 240           | 15            | 200                            | 400                            |
| 240 x 240           | 15            | 140                            | 280                            |
| 424 x 240           | 15            | 220                            | 440                            |
| 640 x 360           | 15            | 400                            | 800                            |
| 360 x 360           | 15            | 260                            | 520                            |
| 640 x 360           | 30            | 600                            | 1200                           |
| 360 x 360           | 30            | 400                            | 800                            |
| 480 x 360           | 15            | 320                            | 640                            |
| 480 x 360           | 30            | 490                            | 980                            |
| 640 x 480           | 15            | 500                            | 1000                           |
| 480 x 480           | 15            | 400                            | 800                            |
| 640 x 480           | 30            | 750                            | 1500                           |
| 480 x 480           | 30            | 600                            | 1200                           |
| 848 x 480           | 15            | 610                            | 1220                           |
| 848 x 480           | 30            | 930                            | 1860                           |
| 640 x 480           | 10            | 400                            | 800                            |
| 1280 x 720          | 15            | 1130                           | 2260                           |
| 1280 x 720          | 30            | 1710                           | 3420                           |
| 960 x 720           | 15            | 910                            | 1820                           |
| 960 x 720           | 30            | 1380                           | 2760                           |
| 1920 x 1080         | 15            | 2080                           | 4160                           |
| 1920 x 1080         | 30            | 3150                           | 6300                           |
| 1920 x 1080         | 60            | 4780                           | 6500                           |
| 2560 x 1440         | 30            | 4850                           | 6500                           |
| 2560 x 1440         | 60            | 6500                           | 6500                           |
| 3840 x 2160         | 30            | 6500                           | 6500                           |
| 3840 x 2160         | 60            | 6500                           | 6500                           |


### API 参考
* [`setVideoEncoderConfiguration`](https://docs.agora.io/cn/Video/API%20Reference/oc/v2.4/Classes/AgoraRtcEngineKit.html#//api/name/setVideoEncoderConfiguration:)
* 关于视频的方向模式，更多信息请参考[视频采集旋转](../../cn/Video/rotation_guide_ios.md)。

## 开发注意事项
- [`degradationPreference`](https://docs.agora.io/cn/Video/API%20Reference/oc/v2.4/Classes/AgoraVideoEncoderConfiguration.html#//api/name/degradationPreference) 参数设置为 `AgoraDegradationMaintainQuality`，表示带宽受限时，降低编码帧率以保证视频质量。此时开发者可以使用 `minFrameRate` 参数设置当前最低的编码帧率，用于平衡帧率和视频质量。通常来说：

	- `minFrameRate` 较低时，一旦带宽不足，帧率下降幅度较大，画质清晰度受影响比较小
	- `minFrameRate` 较高时，一旦带宽不足，帧率下降幅度有限，画质清晰度受影响比较大

 请确保 `minFrameRate` 的值不超过 `frameRate` 的值。`minFrameRate` 的系统默认值是经过试验且能满足一般情况下的需求，我们建议用户不要修改该参数的默认值。
- 如果用户加入频道后不需要重新设置视频编码属性，建议在 `enableVideo` 前调用 `setVideoEncoderConfiguration` ，可以加快首帧出图的时间。
- Agora SDK 会根据实时网络环境，对设置的参数作自适应调整，通常会下调参数。
- 通常的，直播场景下需要较大码率来提升视频质量。因此 Agora 建议将直播码率值设为通信值的 2 倍。详情请参考[设置码率](https://docs.agora.io/cn/Video/API%20Reference/oc/Classes/AgoraVideoEncoderConfiguration.html#//api/name/bitrate)。 
- 直播模式通常需要更大的码率来支持清晰度，因此建议主播使用较稳定的网络。
- 本文中各参数的设置可能会影响计费，详情请参考[计费](../../cn/Agora%20Platform/billing_faq.md)。


## 用户常见问题

### 能否推荐一些常用推荐视频分辨率、帧率、码率？

通常来讲，视频参数的选择要根据产品实际情况来确定，比如，如果是1对1 ，老师和学生的窗口比较大，要求分辨率会高一点，随之帧率和码率也要高一点；如果是1对4， 老师和学生的窗口都比较小，分辨率可以低一点，对应的码率帧率也会低一点，以减少编解码的资源消耗和缓解下行带宽压力。一般可按下列场景中的推荐值进行设置。

- 2 人视频通话场景：
  - 分辨率 320*240、帧率 15 fps、码率 200 Kbps 
  - 分辨率 640*360、帧率 15 fps、码率 400  Kbps
- 多人视频通话场景：
  - 分辨率 160*120、帧率 15 fps、码率 65 Kbps
  - 分辨率 320*180、帧率 15 fps、码率 140  Kbps
  - 分辨率 320*240、帧率 15 fps、码率 200 Kbps

如果你希望自定义视频参数，比如调高码率以保证视频质量，也可以使用 `setVideoEncoderConfiguration` 对各参数进行自定义设置。
