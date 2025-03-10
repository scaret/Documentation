
---
title: 发版说明
description: 
platform: Android
updatedAt: Thu Jun 06 2019 10:00:55 GMT+0800 (CST)
---
# 发版说明
## 简介

Agora RTM SDK 提供了稳定可靠、低延时、高并发的全球消息云服务，帮助你快速构建实时通信场景,  可实现消息通道、呼叫、聊天、状态同步等功能。点击 [实时消息产品概述](../../cn/Real-time-Messaging/RTM_product.md) 了解更多详情。

## 0.9.3 版

该版本于 2019 年 6 月 7 日发布。

### 新增功能

#### 发送（离线）点对点消息

本版本支持发送离线消息。在开通离线消息后，用户不必等到接收端上线才能发送点对点消息。如果对端离线，消息服务器会为每个接收端存储 200 条离线消息长达七天。消息以队列形式存储。当离线消息超限时，最新存储的消息会导致最老的消息丢失。当发送端设置了离线消息，而此时消息接收端不在线，发送端会收到错误码：[PEER_MESSAGE_ERR_CACHED_BY_SERVER](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_peer_message_error.html#a723c2bc0bb1d4b045edc4044f026e30c)

> 该方法的调用频率限制为每秒 60 条（点对点消息和频道消息一并计算在内）。

#### 设置本地用户属性、查询指定用户属性

本版本支持设置和查询用户属性。每个用户属性为 key 和 value 的键值对。每个属性的 key 为 32 字节可见字符，每个属性的 value 的字符串长度不得超过 8 KB。单个用户的全部属性长度不得超过 16 KB。以下为本版本支持内容：

   - 全量设置本地用户属性
   - 增加或更新本地用户属性
   - 删除本地用户指定属性
   - 清空本地用户属性
   - 全量获取指定用户属性
   - 获取指定用户指定属性。


> - 用户属性的相关操作必须在登录 Agora RTM 系统成功后才能进行，否则 SDK 会返回错误码：`ATTRIBUTE_OPERATION_ERR_NOT_READY`
> - 设置的用户属性会在用户登出 Agora RTM 系统后自动失效。
> - 单次用户属性设置操作不得超过 16 KB，否则 SDK 会返回错误码：`ATTRIBUTE_OPERATION_ERR_SIZE_OVERFLOW` 。
> - 用户属性设置相关操作的调用频率限制为每 5 秒 10 条，超限则 SDK 会返回错误码：`ATTRIBUTE_OPERATION_ERR_TOO_OFTEN`。
> - 获取用户属性相关操作的调用频率为每 5 秒 40 条，超限则 SDK 会返回错误码：`ATTRIBUTE_OPERATION_ERR_TOO_OFTEN` 。

### API 变更

#### 新增：

- [sendMessageToPeer()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a729079805644b3307297fb2e902ab4c9):  发送（离线）点对点消息给指定用户。
- [getServerReceivedTs()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_message.html#a7994de6da26269c3137e93ddf7a2c2be)： 消息接收者查询服务器的接收消息时间。
- [isOfflineMessage()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_message.html#a463b5df7c54bf45dc39aa42457e4b5bd)：消息接收者查询消息是否为离线消息。
- [PEER_MESSAGE_ERR_CACHED_BY_SERVER](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_peer_message_error.html#a723c2bc0bb1d4b045edc4044f026e30c)：对端用户不在线，离线消息会被消息服务器存储。
- [setLocalUserAttributes()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a339b7b2371ff2b86137b6db6c1c66294)：全量设置本地用户属性
- [addOrUpdateLocalUserAttributes()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a765b186d62ed3ef6d67a5e875b040875)：增加本地用户属性或更新本地用户属性
- [deleteLocalUserAttributesByKeys()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a2477533989c1bb9ced831af210f1dba4)：删除本地用户指定属性
- [clearLocalUserAttributes()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#ae0c6c5c5bae6020e69009441d8a41785)：清空本地用户全部属性
- [getUserAttributes()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#aee9a6c027f35b652781f654a89433755)：获取指定用户的全部属性
- [getUserAttributesByKeys()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a3b927c35cca5ebd31afb976d60e99193): 获取指定用户的指定属性
- [	AttributeOperationError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_attribute_operation_error.html)：属性操作相关错误码

### 性能改进

- 支持在登录 Agora RTM 系统之前创建频道实例。
- 取消创建 RTM 频道最多 20 个的限制，但是同一用户只能同时加入 20 个频道，超限后会收到错误码 `JOIN_CHANNEL_ERR_FAILURE ` 。


### 问题修复

- 偶现的系统崩溃。
- 用户登出后，其它用户查询该用户仍然显示在线，30 秒后查询不在线。

## 0.9.2 版

该版本于 2019 年 5 月 8 日发布。

> 当前版本不支持在 [登录](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a995bb1b1bbfc169ee4248bd37e67b24a) RTM 系统前 [创建频道实例](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a95ebbd1a1d902572b444fef7853f335a) 。

### 新增功能

#### 查询用户在线状态

本版本引入了新的概念：在线和离线。一般情况下：

- 在线：用户已登录到 Agora RTM 系统。
- 离线：用户已登出 Agora RTM 系统或因其他原因，比如权限或网络原因，与 Agora RTM 系统断开连接。

本版本增加了查询用户在线状态功能。你可以在登录 Agora RTM 系统后查询最多 256 个指定用户的在线状态。详见： [queryPeersOnlineStatus](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#ac711f981405648ed5ef1cb07436125f3) 接口。

> - 返回的 Map 的 Use ID 的顺序以输入顺序为准。
> - 返回的 Map 中与每个 User ID 对应的 BOOLEAN 值表示用户在线与否。
> - 该方法的调用频率限制为每 5 秒 10 次。详见 [限制条件](../../cn/Real-time-Messaging/RTM_limitations_ios.md) 。


#### 更新 Token

在安全性要求较高的情况下，你需要输入 Token [登录](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a995bb1b1bbfc169ee4248bd37e67b24a) Agora RTM 系统。 每个 Token 都会在生成 24 小时后过期，本版本提供了 [更新 Token](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a9a6d33282509384165709107d7a89353) 的功能。

- 在登录 Agora RTM 系统时，如果你的 Token 已过期，SDK 会返回 [LOGIN_ERR_TOKEN_EXPIRED](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_login_error.html#a4a15940de40fe029ba9821e406f3d875) 错误码
- 在已登录 Agora RTM 系统的情况下，Token 过期不会导致用户立即被踢出，但当用户重新登录 Agora RTM 系统时需要调用。所以，我们建议你在收到 [onTokenExpired](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_client_listener.html#aef74f37ed8797d274115d7f13785134e) 回调后尽快更新 Token。


> - [renewToken](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a9a6d33282509384165709107d7a89353) 方法必须在 [创建 RtmClient 实例](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a6411640143c4d0d0cd9481937b754dbf) 后才能调用。
> - Agora RTM Token 的生成方式、输入参数与 Agora 媒体 SDK 不同，详情请见： [校验用户权限](../../cn/Real-time-Messaging/RTM_key.md) 。
> - `RenewToken` 方法的调用频率限制为 2 次 / 秒。详见 [限制条件](../../cn/Real-time-Messaging/RTM_limitations_ios.md) 。

### 性能改进

- 支持以空格开头的 `userId` 参数。


### API 变更

#### 查询用户在线状态相关

##### 新增

- 方法： [queryPeersOnlineStatus](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#ac711f981405648ed5ef1cb07436125f3)
- 错误码：[QueryPeersOnlineStatusError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_query_peers_online_status_error.html)

#### 更新 Token 相关

##### 新增

- 方法： [renewToken](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html#a9a6d33282509384165709107d7a89353)
- 回调： [onTokenExpired](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_client_listener.html#aef74f37ed8797d274115d7f13785134e)
- 错误码： [RenewTokenError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_renew_token_error.html)

#### 呼叫邀请相关

新增以下错误码覆盖用户在没有登录 Agora RTM 系统的情况下发送呼叫邀请的错误情况：

- [LOCAL_INVITATION_ERR_NOT_LOGGEDIN](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_local_invitation_error.html#aa717afb5d4809544e6d66e1c0538f2eb)


## 0.9.1 版

该版本于 2019 年 4 月 4 日发布。

> 本版本不包含 `setLogFile` 和 `setLogFilter` 方法。所有的日志信息默认保存在 **/sdcard/\<AppName\>/agorartm.log** 。

### 新增功能

本版本增加了呼叫邀请功能。结合音视频一对一或一对多通话场景，你可以创建、发送、取消、接受或拒绝一个呼叫邀请。

### 性能改进

- 优化了对象关系帮助开发者快速搭建应用。
- 重命名部分接口以遵循 Java 命名规范。
- 删除状态 `ChannelMessageState` 和 `PeerMessageState` 以简化发送频道消息和点对点消息流程。以错误码 `ChannelMessageError` 和 `PeerMessageError` 代替。
- 删除用于监听消息状态的 `IStateListener` 类。改用 `ResultCallback` 类返回成功和错误回调。

### API 变更

#### 新增

- [LocalInvitation.setContent()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_local_invitation.html#a4cec28ff6d356242329b1034c7531445): 用于主叫设置发出的呼叫邀请内容。
- [LocalInvitation.getContent()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_local_invitation.html#a97294ce1b9b591f9d93e497869b1ad90): 用于主叫获取发出的呼叫邀请内容。 
- [LocalInvitation.getResponse()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_local_invitation.html#a268c738458538a266d440b0e281328ee): 用于主叫获取被叫对发出呼叫邀请的响应内容。
- [LocalInvitation.getState()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_local_invitation.html#a59608fbac8050f17ec0f855f28598d20): 用于主叫获取发出的呼叫邀请的状态。 
- [RemoteInvitation.getCallerId()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_remote_invitation.html#ae38c5740aa9edb09749f0febb2663926): 用于被叫获取主叫的用户 ID。
- [RemoteInvitation.getContent()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_remote_invitation.html#aeca3b3e981c69c44c7a618d4fdfb3b87): 用于被叫获取主叫设置的呼叫邀请内容。
- [RemoteInvitation.setResponse()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_remote_invitation.html#a229b8cf773eaa0e79b0d67815fd6b6f1): 用于被叫设置呼叫邀请响应。 
- [RemoteInvitation.getResponse()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_remote_invitation.html#a12a70e7d8a77eee21d37bbb65b2f9d3e): 用于被叫获取设置的呼叫邀请响应。
- [RemoteInvitation.getState()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_remote_invitation.html#af77a4afabb19ff1468edf29720361a0f): 用于被叫获取收到的呼叫邀请的状态。
- [RtmCallEventListener.onLocalInvitationReceivedByPeer()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a24e1cb71d3e752963da49bdf91847788): 被叫收到呼叫邀请回调。 
- [RtmCallEventListener.onLocalInvitationAccepted()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a4dece02a62a187a66c2415fecf6b75dc): 被叫已接受呼叫邀请回调。 
- [RtmCallEventListener.onLocalInvitationRefused()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a6224643c400268d356cb5d489825bdd0): 被叫已拒绝呼叫邀请回调。 
- [RtmCallEventListener.onLocalInvitationCanceled()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#ae3164e81772cd4d6171165b1705adcaa): 呼叫邀请已取消回调。 
- [RtmCallEventListener.onLocalInvitationFailure()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#acfefb97eaca497cbd71a0c1cbf5067b0): 发出的呼叫邀请进程失败回调。 
- [RtmCallEventListener.onRemoteInvitationReceived()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a8d01498a993c4016aa45ccb9bf4e9097): 收到呼叫邀请回调。 
- [RtmCallEventListener.onRemoteInvitationAccepted()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a81d9d3de89d08c41408d8a94c8309d29): 已接受呼叫邀请回调。 
- [RtmCallEventListener.onRemoteInvitationRefused()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a7a21eaa9ff49bcf39e3c49b94f6e6ac7): 已拒绝呼叫邀请回调。 
- [RtmCallEventListener.onRemoteInvitationCanceled()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a9d0409c87455d4d2b1315f67a5f7aa12): 主叫已取消呼叫邀请回调。 
- [RtmCallEventListener.onRemoteInvitationFailure()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_call_event_listener.html#a6f9f2bbbfbcb0a766c6f1b2e4a8314a1): 发给被叫的呼叫邀请进程失败回调。 
- [RtmCallManager.setEventListener()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_call_manager.html#a934eee4922584707a1a7ef9ac6999cf2): 设置 `RtmCallManager` 实例的事件监听。
- [RtmCallManager.createLocalInvitation()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_call_manager.html#a1756dca077267acaa407c6901daa2248): 创建呼叫邀请。 
- [RtmCallManager.sendLocalInvitation()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_call_manager.html#af899697061305ca840e829b92c78e353): 向指定用户发送呼叫邀请。 
- [RtmCallManager.acceptRemoteInvitation()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_call_manager.html#a5f6f97c84e426e2fbd8a5dda71e2fc6c): 用于被叫接受呼叫邀请。 
- [RtmCallManager.refuseRemoteInvitation()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_call_manager.html#a2ce4af944183976d18c055816f756bf6): 用于被叫拒绝呼叫邀请。 
- [RtmCallManager.cancelLocalInvitation()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_call_manager.html#a5f03bfe1cfd6987fbc7b5a4dc484f564): 用于主叫取消呼叫邀请。 
- [RtmStatusCode#LocalInvitationState](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_local_invitation_state.html): 返回给主叫的呼叫邀请状态码。
- [RtmStatusCode#RemoteInvitationState](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_remote_invitation_state.html): 返回给被叫的呼叫邀请状态码。 
- [RtmStatusCode#LocalInvitationError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_local_invitation_error.html): 返回给主叫的呼叫邀请错误码。 
- [RtmStatusCode#RemoteInvitationError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_remote_invitation_error.html): 返回给主叫的呼叫邀请错误码。 
- [RtmStatusCode#InvitationApiCallError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_invitation_api_call_error.html): 呼叫邀请相关 API 方法调用的错误码。 
- [ConnectionChangeReason#CONNECTION_CHANGE_REASON_REMOTE_LOGIN](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_connection_change_reason.html): 另一个实例已用相同的用户 ID 登录 Agora RTM 系统。

#### 重命名

- 将用于释放 `RtmClient` 实例的所有资源的 `RtmClient.destroy()` 方法更名为 [RtmClient.release()](../../API%20Reference/RTM_java/classio_1_1agora_1_1rtm_1_1_rtm_client.html.md) 。
- 将 `IResultCallback` 类更名为 [ResultCallback](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_result_callback.html) 类。

#### 删除

- 从 [PeerMessageError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_peer_message_error.html) 删除 `PEER_MESSAGE_RECEIVED_BY_SERVER` ，改用错误码  `PEER_MESSAGE_ERR_OK` 。
- 从 [ChannelMessageError](../../API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_channel_message_error.html.md) 删除 `CHANNEL_MESSAGE_RECEIVED_BY_SERVER`  ，改用错误码 `CHANNEL_MESSAGE_OK` 。
- 删除 `PeerMessageState` 接口，改用 [PeerMessageError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_peer_message_error.html) 。
- 删除 `ChannelMessageState` 接口，改用 [ChannelMessageError](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_rtm_status_code_1_1_channel_message_error.html) 返回频道消息错误码。
- 删除用于监听消息状态的 `IStateListener` 类，改用 [ResultCallback](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_result_callback.html) 类监听点对点消息和频道消息结果。
  - 成功：SDK 返回 [ResultCallback.onSuccess()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_result_callback.html#a7206b30500655c4a73d146acf50cb6f5) 回调。
  - 失败：SDK 返回 [ResultCallback.onFailure()](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_java/interfaceio_1_1agora_1_1rtm_1_1_result_callback.html#a1f9145a3eb119e32cfc0afa938062396) 回调以及相应的错误码

## 0.9.0 版

该版本于 2019 年 2 月 4 日发布。

首次发布。

关键功能

- 发送或接收点对点消息。
- 加入或离开频道。
- 发送或接收频道消息。
