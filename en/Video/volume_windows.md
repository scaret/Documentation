
---
title: Adjust the Volume
description: How to adjust volume
platform: Windows
updatedAt: Mon Jun 10 2019 02:48:07 GMT+0800 (CST)
---
# Adjust the Volume
## Introduction

When using the Agora SDK, you can adjust the audio recording and playback volumes for customization. For example, you can mute the remote audio by setting the volume as 0.

This article describes the scenarios when you need to adjust the volume, the corresponding APIs and considerations in the process from audio recording to playing. 

![](https://web-cdn.agora.io/docs-files/1548729217285)

## Implementation
Before proceeding, ensure that you prepare the development environment. See [Integrate the SDK](../../en/Video/windows_video.md).

### Set the Recording Volume

**Recording** is the process in which audio signals are captured by recorders and transported to signal senders. You can change the recording volume by adjusting the **volume of the recording device** or the **volume of the recording signal**. On Windows, Agora recommends adjusting the recording volume with related APIs.

#### Adjust the Volume of the Recording Device

The value of the volume ranges between 0 and 255. 0 represents the recording device is muted, and 255 is the maiximum volume.

```cpp
// Sets the volume of the recording device.
int setRecordingDeviceVolume(int volume);
```

The value of `volume` corresponds to the **microphone array** on Windows, and 255 is the maximum value, as shown in the following screenshot.

![](https://web-cdn.agora.io/docs-files/1545634908852)

#### Adjust the Volume of the Recording Signal 

If the above methods do not meet your requirements, the Agora SDK provides methods to adjust the volume of the recording signals, which enables adjusting the recording volumes.
The value of the volume ranges between 0 and 400. 100 (default) represents the original volume, and 400 is four times the original volume (amplifying the audio signals by four times).

```cpp
// Initializes the parameter engine.
RtcEngineParameters rep(*lpAgoraEngine);
  
// Sets the volume of the recording signal to 200.
int ret = rep.adjustRecordingSignalVolume(200);
```

#### API Reference
- [`setRecordingDeviceVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_i_audio_device_manager.html#ac24424e86ded2727a532df739ebf8086)
- [`adjustRecordingSignalVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#aa9e9b5ae052022fe2e81232b9e6e7290)

### Set the Playback Volume

**Playback** is the process in which audio signal are transported from signal senders to receivers and then to the players. During this process, you can adjust the volume by changing the **volume of the playback device** or the **volume of the playback signal**. Agora recommends adjusting the playback volume with related APIs. 

#### Adjust the Volume of the Playback Device
The value of the volume ranges between 0 and 255. 0 represents the recording device is muted, and 255 is the maiximum volume.

```cpp
// Sets the volume of the playback device.
int setPlaybackDeviceVolume(int volume);
```

The value of `volume` corresponds to the **louderspearker/headset** on Windows, and 255 is the maximum value, as shown in the following screenshot.

![](https://web-cdn.agora.io/docs-files/1545635853077)

#### Adjust the Volume of the Playback Signal

If the above methods do not meet your requirements, the Agora SDK provides methods to adjust the volume of the playback signals, which enables adjusting the playback volumes.
The value of the volume ranges between 0 and 400. 100 (default) represents the original volume, and 400 is four times the original volume (amplifying the audio signals by four times).

```cpp
// Initializes the parameter engine.
RtcEngineParameters rep(*lpAgoraEngine);

// Sets the volume of the playback signal to 200.
int ret = rep.adjustPlaybackSignalVolume(200);
```

#### API Reference

- [`setPlaybackDeviceVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a20b66e126ff710afc0e9258f96be8e7a)
- [`adjustPlaybackSignalVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a8bed09e12b8e2d9934aafad50b77d364)

### Set the Audio Mixing Volume

**Audio mixing** is playing local or online music while speaking, so that other users in the channel can hear the speaker and the music simultaneously. See [Audio Mixing](../../en/Video/effect_mixing_windows.md) for enabling this function.

The value of the audio mixing volume ranges between 0 and 100. 100 (default) represents the original volume, and 0 means the audio mixing is muted.

```cpp
// Initializes the parameter engine.
RtcEngineParameters rep(*lpAgoraEngine);

// Sets the audio mixing volume for the remote users.
int ret = rep.adjustAudioMixingPublishVolume(50);
// Sets the audio mixing volume for both local users. 
int ret = rep.adjustAudioMixingPlayoutVolume(50);
```

You can also call the API `adjustAudioMixingVolume` to set the volume of audio playing for both remote users and local users.

```cpp
// Initializes the parameter engine.
RtcEngineParameters rep(*lpAgoraEngine);

// Sets the audio mixing volume for both local and remote users.
int ret = rep.adjustAudioMixingVolume(50);
```

#### API Reference

- [`adjustAudioMixingPublishVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a8f8d2af4b4c7988934e152e3b281d734)
- [`adjustAudioMixingPlayoutVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a99ab2878e0c4fbf1be6970a2c545d085)
- [`adjustAudioMixingVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a5e117be71d38d813208198f4064aa964)

### Set the Audio Effects Volume

 **Audio effects** are certain short-time sounds such as clapping and gunshots. See [Audio Effects](../../en/Video/effect_mixing_windows.md) for enabling this function.

The value of the audio effects volume ranges between 0.0 and 100.0. 100 .0 (default) represents the original volume, and 0.0 means the audio effect is muted.

```cpp
// Initializes the parameter engine.
RtcEngineParameters rep(*lpAgoraEngine);

// Sets the volume of all audio effect files.
int ret = rep.setEffectsVolume(50);
// Sets the volume of a single audio effect file.
int ret = rep.setVolumeOfEffect(soundId, 50);
```

#### API Reference

- [`setEffectsVolume`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#aa3041ef19bfe10ffc5a1130cda91ab7b)
- [`setVolumeOfEffect`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a71fac1633ea84c892879781bee56d001)

### Get the Data of the Loudest Speaker (Callback Method)

In audio recording, mixing and playing, you can use the following APIs to get the data of the loudest speaker in the channel.

- The speakers with the highest instant volume

```cpp
void onAudioVolumeIndication(const AudioVolumeInfo* speakers, unsigned int speakerNumber, int totalVolume)  {
// Gets the ID of the speakers with the highest instant volume. A user ID of 0 indicates it is the local user.
// speakers is an array that contains uid and volumne of the speaker, volume ranging between 0 and 255.
// speakerNumber shows the size of the speakers array.
// totalVolume is the toal volume after audio mixing, ranging between 0 to 255.
}
```

- The speaker with the highest accumulative volume during a certain period


```cpp
void onActiveSpeaker(uid_t uid) {
// Gets the ID of the speaker with the highest accumulative volume during a certain period. A user ID of 0 indicates it is the local user.
}
```

#### API Reference

- [`onAudioVolumeIndication`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a59ae67333fbc61a7002a46c809e2ec4f)
- [`onActiveSpeaker`](https://docs.agora.io/en/Video/API%20Reference/cpp/classagora_1_1rtc_1_1_i_rtc_engine_event_handler.html#ae643c9dbf94360a23a8b3a56c93f90bc)

## Considerations

- The API methods have return values. If the method call fails, the return value is < 0.
- If the volume of the audio signal is set too high, noise may occur on some devices.

