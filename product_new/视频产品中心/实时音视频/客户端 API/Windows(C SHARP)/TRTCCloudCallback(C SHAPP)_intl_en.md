
TRTCCloudCallback @ TXLiteAVSDK.

__Feature__

Callback API class for TRTC video call feature.



## Common Event Callbacks
### onError

Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions.
```
void onError(TXLiteAVError errCode, string errMsg, IntPtr extraInfo)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| errCode | TXLiteAVError | Error code. |
| errMsg | string | Error message. |
| extraInfo | IntPtr | Extended field. Certain error codes may carry extra information for troubleshooting. |


### onWarning

Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure.
```
void onWarning(TXLiteAVWarning warningCode, string warningMsg, IntPtr extraInfo)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| warningCode | TXLiteAVWarning | Warning code. |
| warningMsg | string | Warning message. |
| extraInfo | IntPtr | Extended field. Certain warning codes may carry extra information for troubleshooting. |



## Room Event Callbacks
### onEnterRoom

Callback of room entry.
```
void onEnterRoom(int result)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| result | int | If `result` is greater than 0, it will be the time used for room entry in ms; if `result` is smaller than 0, it will be room entry error code. |

__Overview__

After the `enterRoom()` API in `TRTCCloud` is called to enter a room, the `onEnterRoom(result)` callback will be received from the SDK.
- If room entry succeeded, `result` will be a positive number (`result` > 0), indicating the time in milliseconds (ms) used for entering the room.
- If room entry failed, `result` will be a negative number (`result` < 0), indicating the error code for room entry failure. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/647/35140).

>?In TRTC versions below 6.6, the `onEnterRoom(result)` callback will be returned only for successful room entry, and [onError()](https://intl.cloud.tencent.com/document/product/647/35138#onerror) will be returned for room entry failure. In TRTC v6.6 and above, a positive `result` will be returned for successful room entry, and a negative `result` together with the [onError()](https://intl.cloud.tencent.com/document/product/647/35138#onerror) callback will be returned for room entry failure.



### onExitRoom

Callback of room exit.
```
void onExitRoom(int reason)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| reason | int | Reason for exiting the room. 0: the user actively called `exitRoom` to exit the room; 1: the user was kicked out of the room by the server; 2: the room was dismissed. |

__Overview__

When the `exitRoom()` API in `TRTCCloud` is called, the logic related to room exit will be executed, such as releasing resources of audio/video devices and codecs. After resources are released, the SDK will use the [onExitRoom()](https://intl.cloud.tencent.com/document/product/647/35138#onexitroom) callback to notify you.
If you need to call `enterRoom()` again or switch to another audio/video SDK, please wait until you receive the [onExitRoom()](https://intl.cloud.tencent.com/document/product/647/35138#onexitroom) callback; otherwise, exceptions such as occupied camera or mic may occur.


### onSwitchRole

Callback of role switching.
```
void onSwitchRole(TXLiteAVError errCode, string errMsg)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| errCode | TXLiteAVError | Error code. `ERR_NULL` indicates a successful switch. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/647/35140). |
| errMsg | string | Error message. |

__Overview__

Calling the `switchRole()` API in `TRTCCloud` will switch between the anchor and viewer roles, which will be accompanied by a line switch process. After the SDK switches the roles, the [onSwitchRole()](https://intl.cloud.tencent.com/document/product/647/35138#onswitchrole) event callback will be returned.


### onConnectOtherRoom

Callback of the result of requesting cross-room call (anchor competition).
```
void onConnectOtherRoom(string userId, TXLiteAVError errCode, string errMsg)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | `userId` of the target anchor to compete with |
| errCode | TXLiteAVError | Error code. `ERR_NULL` indicates a successful switch. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/647/35140). |
| errMsg | string | Error message. |

__Overview__

Calling the `connectOtherRoom()` API in `TRTCCloud` will establish a video call between two anchors in two different rooms, i.e., the "anchor competition" feature. The caller will receive the [onConnectOtherRoom()](https://intl.cloud.tencent.com/document/product/647/35138#onconnectotherroom) callback to see whether the cross-room call is successful; and if yes, all users in both rooms will receive the [onUserVideoAvailable()](https://intl.cloud.tencent.com/document/product/647/35138#onuservideoavailable) callback of anchor competition.


### onDisconnectOtherRoom

Callback of the result of ending cross-room call (anchor competition).
```
void onDisconnectOtherRoom(TXLiteAVError errCode, string errMsg)
```



## Member Event Callbacks
### onRemoteUserEnterRoom

A user enters the current room.
```
void onRemoteUserEnterRoom(string userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |

__Overview__

For the sake of performance, the behaviors of this notification will be different in two different application scenarios:
- Video call scenario (`TRTCAppSceneVideoCall`): users in this scenario do not have different roles, and this notification will be triggered whenever a user enters the room.
- Online LVB scenario (`TRTCAppSceneLIVE`): this scenario does not limit the number of viewers. If any user entering or exiting the room could trigger the callback, it would cause great performance loss. Therefore, this notification will be triggered only when an anchor but not a viewer enters the room.

>?Note: `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` apply only to maintaining the "member list" of the current room. To display the remote image, it is recommended to listen on the [onUserVideoAvailable()](https://intl.cloud.tencent.com/document/product/647/35138#onuservideoavailable) event callback.



### onRemoteUserLeaveRoom

A user exits the current room, which corresponds to `onuserEnterRoom`.
```
void onRemoteUserLeaveRoom(string userId, int reason)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| reason | int | Reason for exiting the room. 0: the user proactively exited the room; 1: the user exited the room due to timeout; 2: the user was kicked out of the room. |

__Overview__

Similar to `onRemoteUserEnterRoom`, the behaviors of this notification will be different in two different application scenarios:
- Video call scenario (`TRTCAppSceneVideoCall`): users in this scenario do not have different roles, and this notification will be triggered whenever a user exits the room.
- Online LVB scenario (`TRTCAppSceneLIVE`): this notification will be triggered only when an anchor but not a viewer exits the room.


### onUserVideoAvailable

Whether camera is enabled for video.
```
void onUserVideoAvailable(string userId, bool available)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| available | bool | Whether image is enabled. |

__Overview__

When the `onUserVideoAvailable(userId, YES)` notification is received, it indicates that available video data frames of the specified image channel have arrived. In this case, the `startRemoteView(userId)` API needs to be called to load the image of the remote user. Then, the callback of rendering the first video frame, i.e., `onFirstVideoFrame(userId)`, will be received.
When the `onUserVideoAvailable(userId, NO)` notification is received, it indicates that the specified channel of remote image has been disabled, which may be because the user called `muteLocalVideo()` or `stopLocalPreview()`.


### onUserSubStreamAvailable

Whether screen sharing is enabled.
```
void onUserSubStreamAvailable(string userId, bool available)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| available | bool | Whether screen sharing is enabled. |

>?The function to display the secondary channel image is `startRemoteSubStreamView()` instead of `startRemoteView()`.



### onUserAudioAvailable

Whether audio upstreaming is enabled.
```
void onUserAudioAvailable(string userId, bool available)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| available | bool | Whether audio is enabled. |


### onFirstVideoFrame

Rendering of the first frame of a local or remote user starts.
```
void onFirstVideoFrame(string userId, TRTCVideoStreamType streamType, int width, int height)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | ID of the local or remote user. `userId == null` indicates the ID of the local user, while `userId != null` indicates the ID of a remote user. |
| streamType | TRTCVideoStreamType | Video stream type: camera or screen sharing. |
| width | int | Image width. |
| height | int | Image height. |

__Overview__

If `userId` is `null`, it indicates that the captured local camera image starts to be rendered, which needs to be triggered by calling `startLocalPreview` first. If `userId` is not `null`, it indicates that the first video frame of the remote user starts to be rendered, which needs to be triggered by calling `startRemoteView` first.

>?This callback will be triggered only after `startLocalPreview()`, `startRemoteView()`, or `startRemoteSubStreamView()` is called.



### onFirstAudioFrame

Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently).
```
void onFirstAudioFrame(string userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | Remote user ID. |


### onSendFirstLocalVideoFrame

The first local video frame data has been sent.
```
void onSendFirstLocalVideoFrame(TRTCVideoStreamType streamType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| streamType | TRTCVideoStreamType | Video stream type: primary image, small image, or secondary stream image (screen sharing). |

__Overview__

The SDK will start capturing the camera and encode the captured image after successful call of `enterRoom()` and `startLocalPreview()`. This callback event will be returned after the SDK successfully sends the first video frame data to the cloud.


### onSendFirstLocalAudioFrame

The first local audio frame data has been sent.
```
void onSendFirstLocalAudioFrame()
```

__Overview__

The SDK will start capturing the mic and encoding the captured audio after successful call of `enterRoom()` and `startLocalAudio()`. This callback event will be returned after the SDK successfully sends the first audio frame data to the cloud.


### onUserEnter

Disused API: an anchor enters the current room.
```
void onUserEnter(string userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |

__Overview__

This callback API can be considered as the disused version of `onRemoteUserEnterRoom` and is not recommended. Please use `onUserVideoAvailable` or `onRemoteUserEnterRoom` for substitution.

>?This API is disused and not recommended.


### onUserExit

Disused API: an anchor exits the current room.
```
void onUserExit(string userId, int reason)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| reason | int | Reason for exit. |

__Overview__

This callback API can be considered as the disused version of `onRemoteUserLeaveRoom` and is not recommended. Please use `onUserVideoAvailable` or `onRemoteUserEnterRoom` for substitution.

>?This API is disused and not recommended.



## Statistics Collection and Quality Callbacks
### onNetworkQuality

Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality.
```
void onNetworkQuality(TRTCQualityInfo localQuality, TRTCQualityInfo[] remoteQuality, uint remoteQualityCount)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| localQuality | [TRTCQualityInfo](https://intl.cloud.tencent.com/document/product/647/35139#trtcqualityinfo) | Upstream network quality. |
| remoteQuality | [TRTCQualityInfo](https://intl.cloud.tencent.com/document/product/647/35139#trtcqualityinfo)[] | Downstream network quality. |
| remoteQualityCount | uint | Array size of the downstream network quality. |

>?`userId == null` indicates the current local video quality.


### onStatistics

Callback of technical metric statistics.
```
void onStatistics(TRTCStatistics statis)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| statis | [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35139#trtcstatistics) | Statistics of local and remote users. |

__Overview__

If you are familiar with audio/video terms, you can use this callback to get all technical metrics of the SDK. If you are developing an audio/video project for the first time, you can focus only on the `onNetworkQuality` callback.

>?The callback is triggered once every 2 seconds.



## Server Event Callbacks
### onConnectionLost

The connection between SDK and server is closed.
```
void onConnectionLost()
```


### onTryToReconnect

The SDK tries to connect to the server again.
```
void onTryToReconnect()
```


### onConnectionRecovery

The connection between SDK and server has been restored.
```
void onConnectionRecovery()
```


### onSpeedTest

Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification.
```
void onSpeedTest(TRTCSpeedTestResult currentResult, uint finishedCount, uint totalCount)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| currentResult | [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35139#trtcspeedtestresult) | Current speed test result. |
| finishedCount | uint | Number of servers on which speed test has been performed. |
| totalCount | uint | Total number of servers on which speed test needs to be performed. |



## Hardware Device Event Callbacks
### onCameraDidReady

Camera is ready.
```
void onCameraDidReady()
```


### onMicDidReady

Mic is ready.
```
void onMicDidReady()
```


### onUserVoiceVolume

Callback of volume level, including the volume level of each `userId` and total remote volume level.
```
void onUserVoiceVolume(TRTCVolumeInfo[] userVolumes, uint userVolumesCount, uint totalVolume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userVolumes | [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35139#trtcvolumeinfo)[] | Volume level of all members who are speaking in the room. Value range: 0–100. |
| userVolumesCount | uint | Number of members in the room. |
| totalVolume | uint | Total volume level of all remote members. Value range: 0–100. |

__Overview__

The `enableAudioVolumeEvaluation` API in `TRTCCloud` can be used to enable this callback or set its triggering interval. It should be noted that after `enableAudioVolumeEvaluation` is called to enable the volume level callback, no matter whether there is a user speaking in the channel, the callback will be called at the set time interval. If there is no one speaking, `userVolumes` will be empty, and `totalVolume` will be `0`.

>?If `userId` is `null`, it indicates the volume level of the local user. `userVolumes` only includes the volume information of users who are speaking (i.e., volume level is not 0).



### onDeviceChange

Callback of local device connection and disconnection.
```
void onDeviceChange(string deviceId, TRTCDeviceType type, TRTCDeviceState state)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| deviceId | string | Device ID. |
| type | [TRTCDeviceType](https://intl.cloud.tencent.com/document/product/647/35139#trtcdevicetype) | Device type. |
| state | [TRTCDeviceState](https://intl.cloud.tencent.com/document/product/647/35139#trtcdevicestate) | Event type. |


### onTestMicVolume

Callback of mic volume level in test.
```
void onTestMicVolume(uint volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint | Volume level. Value range: 0–100. |

__Overview__

The mic test API `startMicDeviceTest` will trigger this callback.


### onTestSpeakerVolume

Callback of speaker volume level in test.
```
void onTestSpeakerVolume(uint volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint | Volume level. Value range: 0–100. |

__Overview__

The speaker test API `startSpeakerDeviceTest` will trigger this callback.



## Custom Message Receipt Callbacks
### onRecvCustomCmdMsg

Callback of receipt of a custom message.
```
void onRecvCustomCmdMsg(string userId, int cmdID, uint seq, byte[] message, uint messageSize)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| cmdID | int | Command ID. |
| seq | uint | Message number. |
| message | byte[] | Message data. |
| messageSize | uint | Message data size. |

__Overview__

When a user in a room uses `sendCustomCmdMsg` to send a custom message, other users in the room can receive the message through the `onRecvCustomCmdMsg` API.


### onMissCustomCmdMsg

Callback of loss of a custom message.
```
void onMissCustomCmdMsg(string userId, int cmdID, int errCode, int missed)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| cmdID | int | Command ID. |
| errCode | int | Error code. |
| missed | int | Number of lost messages. |

__Overview__

TRTC uses the UDP channel; therefore, even if reliable transmission is set, it cannot guarantee that no message will be lost; instead, it can only reduce the message loss rate to a very small value and meet general reliability requirements. After reliable transmission is set on the sender, the SDK will use this callback to notify of the number of custom messages lost during transmission in the specified past time period (usually 5s).


>?Only when reliable transmission is set on the sender can the receiver receive the callback of message loss.


### onRecvSEIMsg

Callback of receipt of an SEI message.
```
void onRecvSEIMsg(string userId, byte[] message, uint messageSize)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| message | byte[] | Data. |
| messageSize | uint | Data size. |

__Overview__

When a user in a room uses `sendSEIMsg` to send data, other users in the room can receive the data through the `onRecvSEIMsg` API.



## CDN Relayed Push Callbacks
### onStartPublishCDNStream

Callback of completion of starting relayed push to CDN.
```
void onStartPublishCDNStream(int errCode, string errMsg)
```

__Overview__

This callback corresponds to the `startPublishCDNStream()` API in `TRTCCloud`.

>?If `Start` callback is successful, the relayed push request has been successfully sent to Tencent Cloud. If the target CDN is exceptional, relayed push may fail.



### onStopPublishCDNStream

Callback of completion of stopping relayed push to CDN.
```
void onStopPublishCDNStream(int errCode, string errMsg)
```

__Overview__

This callback corresponds to the `stopPublishCDNStream()` API in `TRTCCloud`.


### onSetMixTranscodingConfig

Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`.
```
void onSetMixTranscodingConfig(int errCode, string errMsg)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| errCode | int | 0: success; other values: failure. |
| errMsg | string | Specific cause of error. |



## Audio Effect Callbacks
### onAudioEffectFinished

Callback of ending an audio effect.
```
void onAudioEffectFinished(int effectId, int code)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | - |
| code | int | 0 indicates that the audio effect ended normally; other values indicate that the audio effect ended due to exceptions. |



## Screen Sharing Callbacks
### onScreenCaptureCovered

This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away.
```
void onScreenCaptureCovered()
```


### onScreenCaptureStarted

This callback will be returned by the SDK when screen sharing is started.
```
void onScreenCaptureStarted()
```


### onScreenCapturePaused

This callback will be returned by the SDK when screen sharing is paused.
```
void onScreenCapturePaused(int reason)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| reason | int | Reason for pause. 0: the user proactively paused screen sharing; 1: screen sharing parameters were being set; 2: the shared window was minimized; 3: the shared window was hidden. |


### onScreenCaptureResumed

This callback will be returned by the SDK when screen sharing is resumed.
```
void onScreenCaptureResumed(int reason)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| reason | int | Reason for resumption. 0: the user proactively resumed screen sharing; 1: screen sharing automatically resumed after the parameters were set; 2: the minimized shared window was restored; 3: the hidden shared window was restored. |


### onScreenCaptureStoped

This callback will be returned by the SDK when screen sharing is stopped.
```
void onScreenCaptureStoped(int reason)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| reason | int | Reason for stop. 0: the user proactively stopped screen sharing; 1: the shared window was closed. |



## Background Audio Mixing Event Callbacks
### onPlayBGMBegin

Playback of background music starts.
```
void onPlayBGMBegin(TXLiteAVError errCode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| errCode | TXLiteAVError | Error code. |


### onPlayBGMProgress

Progress of background music playback.
```
void onPlayBGMProgress(uint progressMS, uint durationMS)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| progressMS | uint | Elapsed time of the playback. |
| durationMS | uint | Total time. |


### onPlayBGMComplete

Playback of background music ends.
```
void onPlayBGMComplete(TXLiteAVError errCode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| errCode | TXLiteAVError | Error code. |




## ITRTCVideoRenderCallback

__Feature__

Callback of custom video rendering.



### onRenderVideoFrame

Callback of custom video rendering.
```
void onRenderVideoFrame(string userId, TRTCVideoStreamType streamType, TRTCVideoFrame frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | string | User ID. |
| streamType | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideostreamtype) | Stream type, which can be camera or screen sharing. |
| frame | TRTCVideoFrame | Video frame data. |

__Overview__

The `setLocalVideoRenderCallback` and `setRemoteVideoRenderCallback` APIs can be used to set the custom rendering callback.



## ITRTCAudioFrameCallback

__Feature__

Audio data callback.



### onCapturedAudioFrame

Callback of audio data captured by local mic.
```
void onCapturedAudioFrame(TRTCAudioFrame frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | TRTCAudioFrame | Audio data. |

>?
>- Do not perform any time-consuming operation in this callback function. It is recommended to directly copy the data to another thread for processing; otherwise, various audio exceptions will occur.
>- Audio data called back by this API can be modified.
>- The frame time length of audio called back by this API is always 0.02s. The formula to convert the frame time length to frame byte length is **sample rate * frame time length * number of audio channels * sampling point bit width**. For example, the default audio recording format of the SDK has a sample rate of 48,000, mono channel, and sampling point bit width of 16, so its frame byte length will be **48,000 * 0.02s * 1 * 16 bit = 15,360 bit = 1,920 bytes**.
>- The audio data called back by this API includes pre-processing effects such as background music, audio effects, and audio reverb.


### onPlayAudioFrame

Audio data from each remote user before audio mixing (for example, if you want to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing).
```
void onPlayAudioFrame(TRTCAudioFrame frame, string userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | TRTCAudioFrame | Audio data. |
| userId | string | User ID. |

>?
>- Do not perform any time-consuming operation in this callback function. It is recommended to directly copy the data to another thread for processing; otherwise, various audio exceptions will occur.
>- Audio data called back by this API is read only and cannot be modified.


### onMixedPlayAudioFrame

Audio data to be played back by speaker after audio data from each channel is mixed.
```
void onMixedPlayAudioFrame(TRTCAudioFrame frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | TRTCAudioFrame | Audio data. |

>?
>- Do not perform any time-consuming operation in this callback function. It is recommended to directly copy the data to another thread for processing; otherwise, various audio exceptions will occur.
>- Audio data called back by this API can be modified.
>- The frame time length of audio called back by this API is always 0.02s. The formula to convert the frame time length to frame byte length is **sample rate * frame time length * number of audio channels * sampling point bit width**. For example, the default audio playback format of the SDK has a sample rate of 48,000, dual channel, and sampling point bit width of 16, so its frame byte length will be **48,000 * 0.02s * 2 * 16 bit = 30,720 bit = 3,840 bytes**.
>- The audio data called back by this API is the mix of each channel's audio playback data and does not contain the audio data from in-ear monitoring.



## ITRTCLogCallback

__Feature__

Log callback.



### onLog

Callback of log printing.
```
void onLog(string log, TRTCLogLevel level, string module)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| log | string | Log content. |
| level | TRTCLogLevel | Log level. For more information, please see [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35139#trtcloglevel). |
| module | string | Currently, this parameter has no meaning, and its value is always `TXLiteAVSDK`. |


