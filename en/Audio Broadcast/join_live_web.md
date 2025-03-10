
---
title: Join a Channel
description: 
platform: Web
updatedAt: Thu Dec 13 2018 16:11:54 GMT+0800 (CST)
---
# Join a Channel
Before joining the channel, ensure that you prepared the development environment. See [Integrate the SDK](../../en/Interactive%20Broadcast/web_prepare.md).

## Implementation

Once the client initialization is complete, call the `client.join`  method in the `onSuccess` callback.

Pass the channel key, channel name, and user ID to the method parameters:

- `tokenOrKey`: Pass a token that identifies the role and privilege of the user. A token is generated at the server of the app. For how to generate a token, see [Security Keys](../../en/Audio%20Broadcast/token.md). 

	> When creating a project at [Dashboard](https://dashboard.agora.io/), You can generate a Temp Token. A Temp Token can be used at the testing stage. For the production environment, we recommend using a Token generated at your server.
- `channel`: Channel name.
- `uid`: The user ID is an integer and should be unique. If you set the user ID to null, the Agora server assigns a user ID and returns it in the `onSuccess` callback.

```javascript
client.join(<TOKEN_OR_KEY>, <CHANNEL_NAME>, <UID>, function(uid) {
  console.log("User " + uid + " join channel successfully");

}, function(err) {
  console.log("Join channel failed", err);
});
```

> Users with different App IDs cannot call each other even if they join the same channel.

## Next Steps

You are in the channel and can start a live broadcast with the following step:

- [Switch the Client Role](../../en/Interactive%20Broadcast/role_web.md)
- [Publish and Subscribe to Streams](../../en/Interactive%20Broadcast/publish_web_live.md)

For other functions such as manipulating the audio volume, audio effect, or video resolution, you can refer to the following sections:

- [Adjust the Volume](../../en/Interactive%20Broadcast/volume_web.md)
- [Play Audio Effects/Audio Mixing](../../en/Interactive%20Broadcast/effect_mixing_web.md)
- [Set the Video Profile](../../en/Interactive%20Broadcast/videoProfile_web.md)
