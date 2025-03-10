
---
title: 在服务端生成 Token
description: Guide on how to generate tokens on the server side
platform: 服务端
updatedAt: Wed Jun 05 2019 07:47:23 GMT+0800 (CST)
---
# 在服务端生成 Token
本文适用于 2.1 及之后版本的 Agora SDK。通过简单的 API 调用，在服务端生成 Token，在加入频道时使用。

Agora 的鉴权 API 涵盖 Java、Python、CPP、Ruby、Node.js、PHP、Go 语言，你可以根据实际需要，选择相应的语言。

> 声网目前暂不支持用非 0 的 string 型 uid 生成 token。

## Java

### 初始化 Token Builder \(initTokenBuiler\)

```java
public boolean initTokenBuilder(String originToken);
```

该方法初始化 Token Builder。

该方法利用已经存在的 Token，来重新初始化 Token Builder。初始化后，Token Builder 内会包含原来 Token 内的 App ID、App Certificate、 Channel Name、UID 以及 Privilege 信息。

> 如果原先未使用 Token，则无需调用该方法。

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>originToken</code></td>
<td>用户的初始 Token</td>
</tr>
<tr><td>返回值</td>
<td><ul>
<li>0：方法调用成功</li>
<li>&lt; 0：方法调用不成功</li>
</ul>
</td>
</tr>
</tbody>
</table>

Token Builder 的结构体如下所示：

```java
public SimpleTokenBuilder(String appId, String appCertificate, String channelName, String uid);
```

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>appID</code></td>
<td>Agora 为应用程序开发者签发的 App ID。详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App ID</span></a> 。</td>
</tr>
<tr><td><code>appCertificate</code></td>
<td>Agora 为应用程序开发者签发的 App Certificate。当启用 App Certificate 后，原有的 App ID 会失效，详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App Certificate</span></a>。</td>
</tr>
<tr><td><code>channelName</code></td>
<td>标识通话的频道名称，长度在64字节以内的字符串。以下为支持的字符集范围（共89个字符）: a-z,A-Z,0-9,space,! #$%&amp;,()+, -,:;&lt;=.#$%&amp;,()+,-,:;&lt;=.,&gt;?@[],^_,{|},~</td>
</tr>
<tr><td><code>uid</code></td>
<td>用户ID，32位无符号整数。建议设置范围：1到 (2^32-1)，并保证唯一性。如果不指定（即设为0），SDK 会自动分配一个，并在 <code>onJoinChannelSuccess</code> 回调方法中返回，App 层必须记住该返回值并维护，SDK 不对该返回值进行维护</td>
</tr>
</tbody>
</table>


### 生成 Token \(buildToken\)

```java
public String buildToken();
```

该方法创建 Token 。



## C++

### 初始化 Token Builder \(initTokenBuiler\)

```c++
bool initTokenBuilder(const std::string& originToken);
```

该方法初始化 Token Builder。

该方法利用已经存在的 Token，来重新初始化 Token Builder。初始化后，Token Builder 内会包含原来 Token 内的 App ID、App Certificate、 Channel Name、UID 以及 Privilege 信息。

> 如果原先未使用 Token，则无需调用该方法。

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>originToken</code></td>
<td>用户的初始 Token</td>
</tr>
<tr><td>返回值</td>
<td><ul>
<li>0：方法调用成功</li>
<li>&lt;0：方法调用不成功</li>
</ul>
</td>
</tr>
</tbody>
</table>



Token Builder 的结构体如下所示：

```c++
SimpleTokenBuilder();
SimpleTokenBuilder(const std::string& appId, const std::string& appCertificate,
                   const std::string& channelName, uint32_t uid = 0);
SimpleTokenBuilder(const std::string& appId, const std::string& appCertificate,
                   const std::string& channelName, const std::string& uid = "");
```

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>appID</code></td>
<td>Agora 为应用程序开发者签发的 App ID。详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App ID</span></a>     。</td>
</tr>
<tr><td><code>appCertificate</code></td>
<td>Agora 为应用程序开发者签发的 App Certificate。当启用 App Certificate 后，原有的 App ID 会失效，详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App Certificate</span></a> 。</td>
</tr>
<tr><td><code>channelName</code></td>
<td>标识通话的频道名称，长度在64字节以内的字符串。以下为支持的字符集范围（共89个字符）: a-z,A-Z,0-9,space,! #$%&amp;,()+, -,:;&lt;=.#$%&amp;,()+,-,:;&lt;=.,&gt;?@[],^_,{|},~</td>
</tr>
<tr><td><code>uid</code></td>
<td>用户 ID，32 位无符号整数。建议设置范围：1到 (2^32-1)，并保证唯一性。如果不指定（即设为0），SDK 会自动分配一个，并在 <code>onJoinChannelSuccess</code> 回调方法中返回，App 层必须记住该返回值并维护，SDK 不对该返回值进行维护</td>
</tr>
</tbody>
</table>


### 生成 Token \(buildToken\)

```c++
std::string buildToken();
```

该方法生成 Token，Token 的类型为 String。



## Python

### 初始化 Token Builder \(initTokenBuiler\)

```python
def initTokenBuilder(self, originToken);
```

该方法初始化 Token Builder。

该方法利用已经存在的 Token，来重新初始化 Token Builder。初始化后，Token Builder 内会包含原来 Token 内的 App ID、App Certificate、 Channel Name、UID 以及 Privilege 信息。

> 如果原先未使用 Token，则无需调用该方法。

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>originToken</code></td>
<td>用户的初始 Token</td>
</tr>
<tr><td>返回值</td>
<td><ul>
<li>0：方法调用成功</li>
<li>&lt; 0：方法调用不成功</li>
</ul>
</td>
</tr>
</tbody>
</table>

Token Builder 的结构体如下所示：

```python
def __init__(self, appID, appCertificate, channelName, uid);
```

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>appID</code></td>
<td>Agora 为应用程序开发者签发的 App ID。详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App ID</span></a> 。</td>
</tr>
<tr><td><code>appCertificate</code></td>
<td>Agora 为应用程序开发者签发的 App Certificate。当启用 App Certificate 后，原有的 App ID 会失效，详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App Certificate</span></a> 。</td>
</tr>
<tr><td><code>channelName</code></td>
<td>标识通话的频道名称，长度在64字节以内的字符串。以下为支持的字符集范围（共89个字符）: a-z,A-Z,0-9,space,! #$%&amp;,()+, -,:;&lt;=.#$%&amp;,()+,-,:;&lt;=.,&gt;?@[],^_,{|},~</td>
</tr>
<tr><td><code>uid</code></td>
<td>用户ID，32位无符号整数。建议设置范围：1到 (2^32-1)，并保证唯一性。如果不指定（即设为0），SDK 会自动分配一个，并在 <code>onJoinChannelSuccess</code> 回调方法中返回，App 层必须记住该返回值并维护，SDK 不对该返回值进行维护</td>
</tr>
</tbody>
</table>

### 生成 Token\(buildToken\)

```python
def buildToken(self);
```

该方法创建 Token 。



## Go

### 初始化 Token Builder \(initTokenBuiler\)

```go
func (builder SimpleTokenBuilder) InitTokenBuilder(originToken string);
```

该方法初始化 Token Builder。

该方法利用已经存在的 Token，来重新初始化 Token Builder。初始化后，Token Builder 内会包含原来 Token 内的 App ID、App Certificate、 Channel Name、UID 以及 Privilege 信息。

> 如果原先未使用 Token，则无需调用该方法。

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>originToken</code></td>
<td>用户的初始 Token</td>
</tr>
<tr><td>返回值</td>
<td><ul>
<li>0：方法调用成功</li>
<li>&lt;0：方法调用不成功</li>
</ul>
</td>
</tr>
</tbody>
</table>



Token Builder 的结构体如下所示：

```go
func CreateSimpleTokenBuilder(appID, appCertificate, channelName string, uid uint32) SimpleTokenBuilder;
```

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>appID</code></td>
<td>Agora 为应用程序开发者签发的 App ID。详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App ID</span></a> 。</td>
</tr>
<tr><td><code>appCertificate</code></td>
<td>Agora 为应用程序开发者签发的 App Certificate。当启用 App Certificate 后，原有的 App ID 会失效，详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App Certificate</span></a> 。</td>
</tr>
<tr><td><code>channelName</code></td>
<td>标识通话的频道名称，长度在64字节以内的字符串。以下为支持的字符集范围（共89个字符）: a-z,A-Z,0-9,space,! #$%&amp;,()+, -,:;&lt;=.#$%&amp;,()+,-,:;&lt;=.,&gt;?@[],^_,{|},~</td>
</tr>
<tr><td><code>uid</code></td>
<td>用户 ID，32 位无符号整数。建议设置范围：1到 (2^32-1)，并保证唯一性。如果不指定（即设为0），SDK 会自动分配一个，并在 <code>onJoinChannelSuccess</code> 回调方法中返回，App 层必须记住该返回值并维护，SDK 不对该返回值进行维护</td>
</tr>
</tbody>
</table>


### 生成 Token \(buildToken\)

```go
func (builder SimpleTokenBuilder) BuildToken() (string,error);
```

该方法生成 Token。



## PHP

### 初始化 Token Builder \(initTokenBuiler\)

```php
function initTokenBuilder($originToken);
```

该方法初始化 Token Builder。

该方法利用已经存在的 Token，来重新初始化 Token Builder。初始化后，Token Builder 内会包含原来 Token 内的 App ID、App Certificate、 Channel Name、UID 以及 Privilege 信息。

> 如果原先未使用 Token，则无需调用该方法。

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
	<tr><td><code>originToken</code></td>
<td>用户的初始 Token</td>
</tr>
<tr><td>返回值</td>
<td><ul>
<li>0：方法调用成功</li>
<li>&lt; 0：方法调用不成功</li>
</ul>
</td>
</tr>
</tbody>
</table>



Token Builder 的结构体如下所示：

```php
public function __construct($appID, $appCertificate, $channelName, $uid);
```

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>appID</code></td>
<td>Agora 为应用程序开发者签发的 App ID。详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App ID</span></a> 。</td>
</tr>
<tr><td><code>appCertificate</code></td>
<td>Agora 为应用程序开发者签发的 App Certificate。当启用 App Certificate 后，原有的 App ID 会失效，详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App Certificate</span></a> 。</td>
</tr>
<tr><td><code>channelName</code></td>
<td>标识通话的频道名称，长度在64字节以内的字符串。以下为支持的字符集范围（共89个字符）: a-z,A-Z,0-9,space,! #$%&amp;,()+, -,:;&lt;=.#$%&amp;,()+,-,:;&lt;=.,&gt;?@[],^_,{|},~</td>
</tr>
<tr><td><code>uid</code></td>
<td>用户ID，32位无符号整数。建议设置范围：1到 (2^32-1)，并保证唯一性。如果不指定（即设为0），SDK 会自动分配一个，并在 <code>onJoinChannelSuccess</code> 回调方法中返回，App 层必须记住该返回值并维护，SDK 不对该返回值进行维护</td>
</tr>
</tbody>
</table>


### 生成 Token \(buildToken\)

```php
public function buildToken();
```

该方法创建 Token。



## Node.js

### 初始化 Token Builder \(initTokenBuiler\)

```js
initTokenBuilder = function (originToken);
```

该方法初始化 Token Builder。

该方法利用已经存在的 Token，来重新初始化 Token Builder。初始化后，Token Builder 内会包含原来 Token 内的 App ID、App Certificate、 Channel Name、UID 以及 Privilege 信息。

> 如果原先未使用 Token，则无需调用该方法。

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>originToken</code></td>
<td>用户的初始 Token</td>
</tr>
<tr><td>返回值</td>
<td><ul>
<li>0：方法调用成功</li>
<li>&lt;0：方法调用不成功</li>
</ul>
</td>
</tr>
</tbody>
</table>



Token Builder 的结构体如下所示：

```javascript
var SimpleTokenBuilder = function (appID, appCertificate, channelName, uid);
```

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<tbody>
<tr><td><strong>参数</strong></td>
<td><strong>描述</strong></td>
</tr>
<tr><td><code>appID</code></td>
<td>Agora 为应用程序开发者签发的 App ID。详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App ID</span></a> 。</td>
</tr>
<tr><td><code>appCertificate</code></td>
<td>Agora 为应用程序开发者签发的 App Certificate。当启用 App Certificate 后，原有的 App ID 会失效，详见 <a href="../../cn/Audio%20Broadcast/token.md"><span>获取 App Certificate</span></a> 。</td>
</tr>
<tr><td><code>channelName</code></td>
<td>标识通话的频道名称，长度在64字节以内的字符串。以下为支持的字符集范围（共89个字符）: a-z,A-Z,0-9,space,! #$%&amp;,()+, -,:;&lt;=.#$%&amp;,()+,-,:;&lt;=.,&gt;?@[],^_,{|},~</td>
</tr>
<tr><td><code>uid</code></td>
<td>用户 ID，32 位无符号整数。建议设置范围：1到 (2^32-1)，并保证唯一性。如果不指定（即设为0），SDK 会自动分配一个，并在 <code>onJoinChannelSuccess</code> 回调方法中返回，App 层必须记住该返回值并维护，SDK 不对该返回值进行维护</td>
</tr>
</tbody>
</table>


### 生成 Token \(buildToken\)

```javascript
this.buildToken = function ();
```

该方法生成 Token。

