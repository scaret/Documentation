
---
title: Adjust the Volume
description: How to adjust volume on iOS
platform: iOS
updatedAt: Mon Jun 10 2019 02:39:58 GMT+0800 (CST)
---
# Adjust the Volume
## Introduction

When using the Agora SDK, you can adjust the audio recording and playback volumes for customization. For example, you can mute the remote audio by setting the volume as 0.

This page describes the scenarios when you need to adjust the volume, and provides the corresponding APIs and considerations in the process from audio recording to playback. 

![](https://web-cdn.agora.io/docs-files/1548729166359)

## Implementation
Ensure that you prepare the development environment. See [Integrate the SDK](../../en/Video/ios_video.md).

### Set the Recording Volume

**Recording** is a process in which audio signals are captured by recorders and transported to signal senders. During this process, you can adjust the volume by changing the volume of the recording signals with the Agora SDK.

The value of the volume ranges between 0 and 400. 100 (default) is the original volume, and 400 is four times the original volume (amplifying the audio signals by four times).

```swift
// swift
// Sets the volume of the recording signal.
agoraKit.adjustRecordingSignalVolume(50)
```

```objective-c
// objective-c
// Sets the volume of the recording signal.
[agoraKit adjustRecordingSignalVolume: 50];
```

#### API Reference

- [`adjustRecordingSignalVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/adjustRecordingSignalVolume:)

### Set the Playback Volume

**Playback** is a process in which audio signals are transported from signal senders to receivers and then to the players. During this process, you can adjust the volume by changing the volume of the playback signals with the Agora SDK. 

The value of the volume ranges between 0 and 400. 100 (default) is the original volume, and 400 is four times the original volume (amplifying the audio signals by four times).

```swift
// swift
// Sets the volume of the playback signal.
agoraKit.adjustRecordingSignalVolume(50)
```

```objective-c
// objective-c
// Sets the volume of the playback signal.
[agoraKit adjustRecordingSignalVolume: 50];
```

#### API Reference

- [`adjustPlaybackSignalVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/adjustPlaybackSignalVolume:)

### Set the Audio Mixing Volume

**Audio mixing** is playing local or online music while speaking, so that other users in the channel can hear the speaker and the music simultaneously. See [Audio Mixing](../../en/Video/effect_mixing_ios.md) for enabling this function.

The value of the audio mixing volume ranges between 0 and 100. 100 (default) is the original volume, and 0 means the audio mixing is muted.

```swift
// swift
// Sets the audio mixing volume for remote users.
agoraKit.adjustAudioMixingPublishVolume(50)
// Sets the audio mixing volume for local users.
agoraKit.adjustAudioMixingPlayoutVolume(50)
```

```objective-c
// objective-c
// Sets the audio mixing volume for remote users.
[agoraKit adjustAudioMixingPublishVolume: 50];
// Sets the audio mixing volume for local users.
[agoraKit adjustAudioMixingPlayoutVolume: 50];
```

You can also call the `adjustAudioMixingVolume` method to set the volume of audio playback for the remote and local users.

```swift
// swift
// Sets the audio mixing volume for the local and remote users.
agoraKit.adjustAudioMixingVolume(50)
```

```objective-c
// objective-c
// Sets the audio mixing volume for the local and remote users.
[agoraKit adjustAudioMixingVolume: 50];
```

#### API Reference

- [`adjustAudioMixingPublishVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/adjustAudioMixingPublishVolume:)
- [`adjustAudioMixingPlayoutVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/adjustAudioMixingPlayoutVolume:)
- [`adjustAudioMixingVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/adjustAudioMixingVolume:)

### Set the Audio Effects Volume

**Audio effects** are short sounds such as clapping and gunshots. See [Audio Effects](../../en/Video/effect_mixing_ios.md) for enabling this function.

The value of the audio effects volume ranges between 0.0 and 100.0. 100.0 (default) is the original volume, and 0.0 means the audio effect is muted.

```swift
// swift
// Sets the volume of all audio effect files.
agoraKit.setEffectsVolume(50.0)
// Sets the volume of a single audio effect file.
// soundId is ID of the audio effect when you call playEffect.
agoraKit.setVolumeOfEffect(soundId:"1", 50.0)
```

```objective-c
// objective-c
// Sets the volume of all audio effect files.
[agoraKit setEffectsVolume: 50.0];
// Sets the volume of a single audio effect file.
// soundId is ID of the audio effect when you call playEffect.
[agoraKit setVolumeOfEffect: soundId:@"1" volume:50.0];
```

#### API Reference

- [`setEffectsVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setEffectsVolume:)
- [`setVolumeOfEffect`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setVolumeOfEffect:withVolume:)

### Set the In-ear Monitor Volume

In audio recording, mixing, and playback, you can call the `setInEarMonitoringVolume` method to adjust the volume of the in-ear monitor.

The value of the in-ear monitoring volume ranges between 0 and 100. 100 (default) is the original volume, and 0 means the in-ear monitoring is muted.

```swift
// swift
// Enables in-ear monitoring.
agoraKit.enableInearMonitoring(true)
// Sets the in-ear monitor volume.
agoraKit.setInEarMonitoringVolume(50)
```

```objective-c
// objective-c
// Enables in-ear monitoring.
[agoraKit enableInEarMonitoring(true)];
// Sets the in-ear monitor volume,
[agoraKit setInEarMonitoringVolume: 50];
```

#### API Reference

- [`enableInEarMonitoring`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/enableInEarMonitoring:)
- [`setInEarMonitoringVolume`](https://docs.agora.io/en/Video/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setInEarMonitoringVolume:)

### Get the Information of the Loudest Speaker (Callback Method)

In audio recording, mixing, and playback, you can use the following methods to get the information of the loudest speakers in the channel.

- The speakers with the highest instant volume


```swift
// swift
func rtcEngine(_ engine: AgoraRtcEngineKit, reportAudioVolumeIndicationOfSpeakers speakers:
[AgoraRtcAudioVolumeInfo], totalVolume: Int) {
// Gets the ID of the speakers with the highest instant volume. A user ID of 0 indicates it is the local user.
// speakers is an array that contains the uids and volumes of the speakers. The volume ranges between 0 and 255.
// totalVolume is the total volume after audio mixing. The value ranges between 0 and 255.
}
```

```objective-c
// objective-c
- (void)rtcEngine:(AgoraRtcEngineKit *_Nonnull)engine reportAudioVolumeIndicationOfSpeakers:(NSArray<AgoraRtcAudioVolumeInfo*> *_Nonnull)speakers totalVolume:(NSInteger)totalVolume {
// Gets the ID of the speakers with the highest instant volume. A user ID of 0 indicates it is the local user.
// speakers is an array that contains the uids and volumes of the speakers. The volume value ranges between 0 and 255.
// totalVolume is the total volume after audio mixing. The value ranges between 0 and 255.
}
```

- The speaker with the highest accumulative volume during a certain period of time

```swift
// swift
func rtcEngine(_ engine: AgoraRtcEngineKit, activeSpeaker speakerUid: UInt) {
// Gets the ID of the speaker with the highest accumulative volume during a certain period of time. A user ID of 0 indicates it is the local user.
}
```

```objective-c
// objective-c
- (void)rtcEngine:(AgoraRtcEngineKit *_Nonnull)engine activeSpeaker:(NSUInteger)speakerUid {
// Gets the ID of the speaker with the highest accumulative volume during a certain period of time. A user ID of 0 indicates it is the local user.
}
```

#### API Reference

- [`reportAudioVolumeIndicationOfSpeakers`](https://docs.agora.io/en/Video/API%20Reference/oc/Protocols/AgoraRtcEngineDelegate.html#//api/name/rtcEngine:reportAudioVolumeIndicationOfSpeakers:totalVolume:4)
- [`activeSpeaker`](https://docs.agora.io/en/Video/API%20Reference/oc/Protocols/AgoraRtcEngineDelegate.html#//api/name/rtcEngine:activeSpeaker:)

## Considerations

- The API methods have return values. If the method call fails, the return value is < 0.
- If the volume of the audio signal is set too high, noise may occur on some devices.

