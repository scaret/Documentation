
---
title: 设置合流布局
description: 
platform: Linux
updatedAt: Thu May 30 2019 09:18:24 GMT+0800 (CST)
---
# 设置合流布局
Agora 云端录制服务提供三种预设的视频布局：

- [悬浮布局](#float)（默认）。第一个加入频道的用户在屏幕上会显示为大视窗，铺满整个画布，其他用户的视频画面会显示为小视窗，从下到上水平排列，最多 4 行，每行 4 个画面，最多支持共 17 个录制画面。
- [自适应布局](#bestfit)。根据用户的数量自动调整每个画面的大小，每个用户的画面大小一致，最多支持 17 个录制画面。
- [垂直布局](#vertical)。指定一个用户在屏幕左侧显示大视窗画面，其他用户的小视窗画面在右侧垂直排列，最多两列，一列 8 个画面，最多支持共 17 个录制画面。

## 实现方法

在开始云端录制时，通过设置合流布局参数选择一种预设的布局。

- 如果你使用云端录制 SDK [调用 API 录制](../../cn/cloud-recording/cloud_recording_quickstart.md)，在开始云端录制时设置 [`TranscodingConfig`](../../cn/cloud-recording/cloud_recording_api.md) 中的 `layout` 参数
- 如果你使用 demo 通过[命令行录制](../../cn/cloud-recording/cloud_recording_demo.md)，在开始云端录制时设置 `—mixedVideoLayoutType` 参数

## 工作原理

本节详细介绍各个布局方式中用户的画面大小和位置。

无论哪一种布局方式，最多支持共 17 个录制画面。

- 如果频道里总人数超过 17 人，则第 18 个及以后的用户的视频流，不会显示在布局中。
- 如果某用户只发送音频，仍然会占据布局位。
- 画面中数字表示用户加入频道的顺序。如果用户 1 退出频道，用户 2 会占据用户 1 的视窗，依次替补。

### <a name="float"></a>悬浮布局

默认布局方式。小视窗会悬浮在大视窗上面。第一个加入频道的用户在屏幕上会显示为大视窗，铺满整个画布，其他用户按照加入的顺序从屏幕左下角开始依次水平排列显示小视窗，最多 4 行，每行 4 个画面。

- 如果某用户只发送音频，仍然会占据布局位，显示大视窗画面。
- 如果用户的实际视频流分辨率与视窗的长宽比不一致，视频画面会缩放以保证视频的完整性。
- 每个小视窗的宽和高分别为整个画布宽和高的 0.235，相邻小视窗的左右和上下间距分别为整个画布宽和高的 0.012。小视窗距离画布的水平和垂直边距也分别为整个画布宽和高的 0.012。

不同人数下实际布局效果如下图所示。

#### 1 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2019-5-16_15-10-7.png?version=1&modificationDate=1557990615369&api=v2)

#### 2 - 5 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2019-5-16_15-10-37.png?version=1&modificationDate=1557990645667&api=v2)

#### 6 - 9 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2019-5-16_15-11-1.png?version=1&modificationDate=1557990670140&api=v2)

#### 10 - 13 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2019-5-16_15-11-22.png?version=1&modificationDate=1557990690258&api=v2)

#### 14 - 17 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2019-5-16_15-8-44.png?version=1&modificationDate=1557990532458&api=v2)

### <a name="bestfit"></a>自适应布局

在该布局下，布局样式会根据频道人数自适应。每个用户的视窗画面大小一致，均等分布。

- 在下面不同人数的合流布局下，如果频道中人数不足，则剩余的布局位置会空着，显示背景色。
- 如果某用户只发送音频，仍然会占据布局，显示背景色。
- 若实际视频流分辨率与视窗的长宽比不一致，视频画面会裁剪以适配视窗的大小。

不同人数下实际布局效果如下图所示。

#### 1- 4 人

![](https://web-cdn.agora.io/docs-files/1558062852403)

![](https://web-cdn.agora.io/docs-files/1558063212804)

![img](https://confluence.agora.io/download/thumbnails/321323097/image2018-3-2_15-13-11.png?version=1&modificationDate=1519974797896&api=v2)

![](https://web-cdn.agora.io/docs-files/1558063229612)

#### 5 - 9 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2018-3-2_15-17-58.png?version=1&modificationDate=1519975084235&api=v2)

#### 10 - 16 人

![img](https://confluence.agora.io/download/thumbnails/321323097/image2018-3-2_15-22-34.png?version=1&modificationDate=1519975360819&api=v2)

#### 17 人

17 人的画面布局与上面的情况不同，用户画面没有铺满整个画布。

每个用户画面的宽和高分别为总宽度和总高度的 0.2，前四行每行四个用户，画布左右边距均为总宽度的 0.1。第五行居中显示第 17 个用户画面。


![img](https://confluence.agora.io/download/thumbnails/321323097/image2018-3-2_16-56-35.png?version=1&modificationDate=1519981001505&api=v2)

### <a name="vertical"></a>垂直布局

如果你选择了垂直布局，需要在开始录制的时候指定一个 uid 作为大视窗画面。如果你使用云端录制 SDK [调用 API 录制](../../cn/cloud-recording/cloud_recording_quickstart.md)，在开始云端录制时设置 [`TranscodingConfig`](../../cn/cloud-recording/cloud_recording_api.md) 中的 `max_resolution_uid` 参数指定；如果你使用 demo 通过[命令行录制](../../cn/cloud-recording/cloud_recording_demo.md)，在开始云端录制时设置 `—maxResolutionUid` 参数指定。

- Large 表示大视窗画面，显示指定的 UID 用户的视频流；如果未指定或者指定用户未进入频道，Large 区域显示背景色。
- 小视窗画面的排列顺序，是按照加入频道的时间先后顺序。如果用户 small 1 退出频道，用户 small 2 会占据用户 small 1 的视窗，依次替补。
- 在下面不同人数的合图布局下，若频道中人数不足，则剩余的布局位置会空着，显示背景色。
- 如果某用户只发送音频，仍然会占据布局位，显示背景色。
- 若实际视频流分辨率与视窗的长宽比不一致，视频画面会缩放以保证视频的完整性。

#### 1 - 5 人

small 1 - small 4 依次显示在画布右侧, 且不会覆盖 Large 画面。小视窗画面宽度是总宽的 1/5，画面高度是总高的 1/4。

![](https://web-cdn.agora.io/docs-files/1558060680455)

#### 6 - 7 人

small 1 - small 6 依次显示在画布右侧, 且不会覆盖 Large 画面。小视窗画面宽度是总宽的 1/7，画面高度是总高的 1/6。

![](https://web-cdn.agora.io/docs-files/1558060697541)

#### 8 - 9 人

small1 - small 8 依次显示在画布右侧, 且不会覆盖 Large 画面。小视窗画面宽度是总宽的 1/9，画面高度是总高的 1/8。

![](https://web-cdn.agora.io/docs-files/1558060714296)

#### 10 - 17 人

small 1 - small 16 依次显示在画布右侧, 且不会覆盖 Large 画面。小视窗画面宽度是总宽的 1/10，画面高度是总高的 1/8。

![](https://web-cdn.agora.io/docs-files/1558060732460)
