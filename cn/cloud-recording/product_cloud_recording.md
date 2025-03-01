
---
title: 云端录制
description: 
platform: Linux
updatedAt: Mon Jun 10 2019 04:22:56 GMT+0800 (CST)
---
# 云端录制
Agora 云端录制，是 Agora 针对音视频通话、直播研发的录制服务，与 Agora Native SDK （1.7.0 或更高版本） 及 Agora Web SDK (1.12.0 或更高版本) 兼容，通过简单的操作方法，帮助开发者快速、灵活地实现录制服务，实现一对一、一对多的音视频通话或直播的录制。同 Agora 本地服务端录制相比，Agora 云端录制无需部署 Linux 服务器，减轻了研发和运维的压力，更轻量便捷。

有了录制功能，你可以将语音聊天、视频聊天以及直播的内容储存下来，提供给更多的人在方便的时间观看。举个例子，某个用户报名参加了某线上课程，除了在规定的时间段上线听课外，他还可以选择在其他时间段观看课程录像，方便复习或补课。该功能可以通过在客户端配置 Agora 云端录制实现。

## 功能描述

Agora 云端录制支持如下功能：

- Agora Native SDK 和 Agora Web SDK 的高清音视频通话的录制
- 频道内所有用户的音视频合流录制
- 支持多种合流布局
- 第三方云存储


## 适用场景

Agora 云端录制应用广泛，主要可以在以下场景中发挥重要作用：

| 行业     | 适用场景                                                     |
| -------- | ------------------------------------------------------------ |
| 在线教育 | 在 1v1 、1v多 的小班线上课堂中，提供高质量的音视频录制：<li>方便用户在课程结束后，反复观看、收听录制下来的课堂视频或音频，来巩固及复习学习成果；<li>因时间冲突错过上课的用户也可以观看课堂视频或音频进行学习。 |
| 社交直播 | <li>精彩瞬间录制<li>直播回放<li>截图鉴黄                                 |
| 金融行业 | 在开展在线理财、开户、面签等业务时，应国家监管要求，必须提供录音录像服务，形成交易记录的视频，存档备查。 |
| 客服中心 | <li>方便后期用户调研<li>获取相关用户信息<li>客服质量评估                 |
| 远程医疗 | 对远程问诊、在线咨询过程进行在线录制，帮助病人足不出户获取医疗资源，并方便后期诊疗参考等。 |

## 产品特性

Agora 云端录制主要有以下特性：

| 特性     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| 高可靠性 | 全球分布式集群部署，提供高可用性服务。                   |
| 高安全性 | 提供视频通话、数据传输、数据存储等端到端安全保障机制，详情可参考[信息安全说明](https://docs.agora.io/cn/Agora%20Platform/security)。 |
| 兼容性   | 支持第三方云存储：七牛云、阿里云和Amazon S3。  |
| 稳定易用 | 操作方法简单易学，能帮助开发者快速集成上线录制服务。 |


## 计费

使用云端录制 SDK 时，相当于一个“哑客户端”加入频道，订阅需要录制的音视频流。录制的音视频流的[集合分辨率](../../cn/Agora%20Platform/billing_faq.md)分为 Audio、HD、HD+ 三档，根据每档对应的单价，按分钟数计费。具体价格请咨询 sales@agora.io。
	
每个录制任务单独计费。例如，基于同一个频道创建两个录制任务，则会分别计费。

## 相关文档和示例代码

- [集成 SDK](../../cn/cloud-recording/cloud_recording_quickstart.md) 展示了如何集成云端录制 SDK 及基本 API 的调用。
- [运行 Demo](../../cn/cloud-recording/cloud_recording_demo.md) 展示了如何使用云端录制 demo 进行录制。
- [云端录制 API](../../cn/cloud-recording/cloud_recording_api.md) 展示了使用云端录制过程中你可以调用的各 API 及其功能，以及会收到的回调等内容。



 

 
