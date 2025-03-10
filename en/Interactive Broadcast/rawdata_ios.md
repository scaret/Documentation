
---
title: Modify Raw Data
description: 
platform: iOS,macOS
updatedAt: Mon Jun 10 2019 09:24:19 GMT+0800 (CST)
---
# Modify Raw Data
The Agora Raw Data interface is an advanced feature provided in the SDK library for users to obtain the raw voice or video data of the SDK engine. Developers can modify the voice or video data and create special effects to meet their needs.

You can implement a preprocessing stage before sending the data to the encoder and modifying the captured video frames or voice signals. You can also implement a postprocessing stage after sending the data to the decoder and modifying the received video frames or voice signals.

The Agora Raw Data interface is a C++ interface.

## Modify the Raw Voice Data

1. Define `AgoraAudioFrameObserver` by inheriting `IAudioFrameObserver` (the `IAudioFrameObserver` class is defined in `IAgoraMediaEngine.h`). You need the following virtual interfaces:

   For example,

   ```c++
   class AgoraAudioFrameObserver : public agora::media::IAudioFrameObserver
   {
     public:
	   // Occurs when the recorded audio frame is received.
       virtual bool onRecordAudioFrame(AudioFrame& audioFrame) override
       {
         return true;
       }
	   // Occurs when the audio playback frame is received.
       virtual bool onPlaybackAudioFrame(AudioFrame& audioFrame) override
       {
         return true;
        }
	   // Occurs when the audio playback frame of a specified user is received.
       virtual bool onPlaybackAudioFrameBeforeMixing(unsigned int uid, AudioFrame& audioFrame) override
        {
         return true;
        }
	   // Occurs when the mixed recorded and playback audio frame is received.
       virtual bool onMixedAudioFrame(AudioFrame& audioFrame) override
        {
        return true;
        }
   
   };
   ```

   This example returns true for voice preprocessing or postprocessing interfaces. Users can modify the data, if necessary:

   ```c++
   class IAudioFrameObserver
   {
     public:
         enum AUDIO_FRAME_TYPE {
         FRAME_TYPE_PCM16 = 0, //PCM 16bit little endian
         };
     struct AudioFrame {
         AUDIO_FRAME_TYPE type;
         int samples;  //number of samples in this frame
         int bytesPerSample; //number of bytes per sample: 2 for PCM 16
         int channels; // number of channels (data are interleaved if stereo)
         int samplesPerSec; //sampling rate
         void* buffer; //data buffer
         int64_t renderTimeMs;
        };
     public:
         virtual bool onRecordAudioFrame(AudioFrame& audioFrame) = 0;
         virtual bool onPlaybackAudioFrame(AudioFrame& audioFrame) = 0;
         virtual bool onPlaybackAudioFrameBeforeMixing(unsigned int uid, AudioFrame& audioFrame) = 0;
         virtual bool onMixedAudioFrame(AudioFrame& audioFrame) = 0;
   };
   ```

2. Register the voice frame observer to the SDK engine. After creating the `IRtcEngine` object, and before joining a channel, you can register the voice frame observer object.

   ```c++
   AgoraAudioFrameObserver s_audioFrameObserver;
   
   agora::util::AutoPtr<agora::media::IMediaEngine> mediaEngine;
   mediaEngine.queryInterface(*engine, agora::AGORA_IID_MEDIA_ENGINE);
   if (mediaEngine)
   {
     mediaEngine->registerAudioFrameObserver(&s_audioFrameObserver);
   }
   ```

> `engine` can be obtained using the following method. `kit` means `AgoraRtcEngineKit`.
>
> ```c++
> agora::IRtcEngine* rtc_engine = (agora::IRtcEngine*)kit.getNativeHandle;
> agora::util::AutoPtr<agora::media::IMediaEngine> mediaEngine;
> mediaEngine.queryInterface(rtc_engine, agora::AGORA_IID_MEDIA_ENGINE);
> ```

## Modify the Raw Video Data

1. Define `AgoraVideoFrameObserver` by inheriting `IVideoFrameObserver` \(the `IVideoFrameObserver` class is defined in `IAgoraMediaEngine.h`\). You need the following virtual interfaces:

   For example,

   ```c++
   class AgoraVideoFrameObserver : public agora::media::IVideoFrameObserver
   {
     public:
	   // Occurs when the camera captured image is received.
       virtual bool onCaptureVideoFrame(VideoFrame& videoFrame) override
       {
         return true;
       }
	   // Processes the received image of the specified user.
       virtual bool onRenderVideoFrame(unsigned int uid, VideoFrame& videoFrame) override
       {
         return true;
       }
   };
   ```

   This example returns true for voice preprocessing or postprocessing interfaces. Users can modify the data, if necessary：

   ```c++
   class IVideoFrameObserver
   {
     public:
       enum VIDEO_FRAME_TYPE {
       FRAME_TYPE_YUV420 = 0,  //YUV 420 format
       };
     struct VideoFrame {
       VIDEO_FRAME_TYPE type;
       int width;  //width of the video frame
       int height;  //height of the video frame
       int yStride;  //stride of the Y data buffer
       int uStride;  //stride of the U data buffer
       int vStride;  // stride of the V data buffer
       void* yBuffer;  //Y data buffer
       void* uBuffer;  //U data buffer
       void* vBuffer;  //V data buffer
       int rotation; // rotation of this frame (0, 90, 180, 270)
       int64_t renderTimeMs;
       };
     public:
       virtual bool onCaptureVideoFrame(VideoFrame& videoFrame) = 0;
       virtual bool onRenderVideoFrame(unsigned int uid, VideoFrame& videoFrame) = 0;
   };
   ```

2. Register the video frame observer to the SDK engine. After creating the `IRtcEngine` object and enabling the video mode, and before joining a channel, you can register the video frame observer object.

   ```c++
   AgoraVideoFrameObserver s_videoFrameObserver;
   
   agora::util::AutoPtr<agora::media::IMediaEngine> mediaEngine;
     mediaEngine.queryInterface(*engine,agora::AGORA_IID_MEDIA_ENGINE);
     if (mediaEngine)
     {
        mediaEngine->registerVideoFrameObserver(&s_videoFrameObserver);
     }
   ```

> `engine` can be obtained using the following method. `kit` means `AgoraRtcEngineKit`.
> ```c++
> agora::IRtcEngine* rtc_engine = (agora::IRtcEngine*)kit.getNativeHandle;
> agora::util::AutoPtr<agora::media::IMediaEngine> mediaEngine;
> mediaEngine.queryInterface(rtc_engine, agora::AGORA_IID_MEDIA_ENGINE);
> ```
