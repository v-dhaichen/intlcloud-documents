## TRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.

### Basic methods

| API | Description |
|-----|-----|
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/35126#sharedinstance) | Creates [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35126#trtccloud) singleton. |
| [destroySharedInstance](https://intl.cloud.tencent.com/document/product/647/35126#destroysharedinstance) | Terminates [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35126#trtccloud) singleton. |
| [setListener](https://intl.cloud.tencent.com/document/product/647/35126#setlistener) | Sets the `TRTCCloudListener` callback API, through which users can get various status notifications from [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35126#trtccloud). |
| [setListenerHandler](https://intl.cloud.tencent.com/document/product/647/35126#setlistenerhandler) | Sets the queue that drives the [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) callback. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/35126#enterroom) | Enters room. |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/35126#exitroom) | Exits room. |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/35126#switchrole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [ConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35126#connectotherroom) | Requests cross-room call (anchor competition). |
| [DisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35126#disconnectotherroom) | Exits cross-room call. |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/35126#setdefaultstreamrecvmode) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35126#startlocalpreview) | Enables preview image of local video. |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/35126#stoplocalpreview) | Stops local video capture and preview. |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/35126#mutelocalvideo) | Specifies whether to block local video image. |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/35126#startremoteview) | Starts displaying remote video image. |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/35126#stopremoteview) | Stops displaying remote video image. |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/35126#stopallremoteview) | Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/35126#muteremotevideostream) | Pauses receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/35126#muteallremotevideostreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/35126#setvideoencoderparam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35126#setnetworkqosparam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/35126#setlocalviewfillmode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/35126#setremoteviewfillmode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/35126#setlocalviewrotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/35126#setremoteviewrotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/35126#setvideoencoderrotation) | Sets direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server). |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35126#setlocalviewmirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/35126#setvideoencodermirror) | Sets mirror mode of image output by encoder. |
| [setGSensorMode](https://intl.cloud.tencent.com/document/product/647/35126#setgsensormode) | Sets adaptation mode of the g-sensor. |
| [enableEncSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/35126#enableencsmallvideostream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35126#setremotevideostreamtype) | Specifies whether to view the big or small image of the specified `uid`. |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35126#setpriorremotevideostreamtype) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/35126#startlocalaudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/35126#stoplocalaudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/35126#mutelocalaudio) | Mutes local audio. |
| [setAudioRoute](https://intl.cloud.tencent.com/document/product/647/35126#setaudioroute) | Sets audio routing. |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35126#muteremoteaudio) | Mutes user's audio. |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35126#muteallremoteaudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/35126#enableaudiovolumeevaluation) | Enables volume reminder. |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/35126#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/35126#stopaudiorecording) | Stops audio recording. |
| [setSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35126#setsystemvolumetype) | Sets the system volume type used during call. |
| [enableAudioEarMonitoring](https://intl.cloud.tencent.com/document/product/647/35126#enableaudioearmonitoring) | Enables in-ear monitoring. |

### Camera API functions

| API | Description |
|-----|-----|
| [switchCamera](https://intl.cloud.tencent.com/document/product/647/35126#switchcamera) | Switches cameras. |
| [isCameraZoomSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscamerazoomsupported) | Queries whether the current camera supports zoom. |
| [setZoom](https://intl.cloud.tencent.com/document/product/647/35126#setzoom) | Sets zoom factor (focal length) of camera. |
| [isCameraTorchSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscameratorchsupported) | Queries whether the device supports flash (flash mode). |
| [enableTorch](https://intl.cloud.tencent.com/document/product/647/35126#enabletorch) | Enables or disables flash. |
| [isCameraFocusPositionInPreviewSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscamerafocuspositioninpreviewsupported) | Queries whether the device supports setting focus. |
| [setFocusPosition](https://intl.cloud.tencent.com/document/product/647/35127#setfocusposition) | Sets camera focus. |
| [isCameraAutoFocusFaceModeSupported](https://intl.cloud.tencent.com/document/product/647/35127#iscameraautofocusfacemodesupported) | Queries whether the device supports automatic recognition of face position. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [getBeautyManager](https://intl.cloud.tencent.com/document/product/647/35127#getbeautymanager) | Gets the beauty filter management object. |
| [setBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35127#setbeautystyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setFilter](https://intl.cloud.tencent.com/document/product/647/35127#setfilter) | Specifies material filter effect. |
| [setFilterConcentration](https://intl.cloud.tencent.com/document/product/647/35127#setfilterconcentration) | Sets effect level of a filter. |
| [setWatermark](https://intl.cloud.tencent.com/document/product/647/35127#setwatermark) | Adds a watermark. |
| [setEyeScaleLevel](https://intl.cloud.tencent.com/document/product/647/35127#seteyescalelevel) | Sets effect level of the eye enlarging filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceSlimLevel](https://intl.cloud.tencent.com/document/product/647/35127#setfaceslimlevel) | Sets effect level of the face slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceVLevel](https://intl.cloud.tencent.com/document/product/647/35127#setfacevlevel) | Sets effect level of the chin slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceShortLevel](https://intl.cloud.tencent.com/document/product/647/35127#setfaceshortlevel) | Sets effect level of the face shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setChinLevel](https://intl.cloud.tencent.com/document/product/647/35127#setchinlevel) | Sets effect level of the chin lengthening/shortening or shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setNoseSlimLevel](https://intl.cloud.tencent.com/document/product/647/35127#setnoseslimlevel) | Sets effect level of the nose slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setGreenScreenFile](https://intl.cloud.tencent.com/document/product/647/35127#setgreenscreenfile) | Sets green screen video (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [selectMotionTmpl](https://intl.cloud.tencent.com/document/product/647/35127#selectmotiontmpl) | Selects AI animated effect pendant (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setMotionMute](https://intl.cloud.tencent.com/document/product/647/35127#setmotionmute) | Mutes animated effect (it takes effect only in TRTC Commercial edition and is invalid in other editions). |


### Secondary stream API functions

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35127#startremotesubstreamview) | Starts displaying screen sharing image of a remote user. |
| [stopRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35127#stopremotesubstreamview) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://intl.cloud.tencent.com/document/product/647/35127#setremotesubstreamviewfillmode) | Sets display mode of screen sharing image. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://intl.cloud.tencent.com/document/product/647/35127#enablecustomvideocapture) | Enables custom video capture mode. |
| [sendCustomVideoData](https://intl.cloud.tencent.com/document/product/647/35127#sendcustomvideodata) | Delivers the captured video data to the SDK. |
| [setLocalVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35127#setlocalvideorenderlistener) | Sets callback of custom rendering for local video. |
| [setRemoteVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35127#setremotevideorenderlistener) | Sets callback of custom rendering for remote video. |
| [enableCustomAudioCapture](https://intl.cloud.tencent.com/document/product/647/35127#enablecustomaudiocapture) | Enables custom audio capture mode. |
| [sendCustomAudioData](https://intl.cloud.tencent.com/document/product/647/35127#sendcustomaudiodata) | Delivers the captured audio data to the SDK. |
| [setAudioFrameListener](https://intl.cloud.tencent.com/document/product/647/35127#setaudioframelistener) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35127#sendcustomcmdmsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://intl.cloud.tencent.com/document/product/647/35127#sendseimsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://intl.cloud.tencent.com/document/product/647/35127#playbgm) | Starts background music. |
| [stopBGM](https://intl.cloud.tencent.com/document/product/647/35127#stopbgm) | Stops background music. |
| [pauseBGM](https://intl.cloud.tencent.com/document/product/647/35127#pausebgm) | Pauses background music. |
| [resumeBGM](https://intl.cloud.tencent.com/document/product/647/35127#resumebgm) | Resumes background music. |
| [getBGMDuration](https://intl.cloud.tencent.com/document/product/647/35127#getbgmduration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://intl.cloud.tencent.com/document/product/647/35127#setbgmposition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://intl.cloud.tencent.com/document/product/647/35127#setmicvolumeonmixing) | Adjusts the mic volume level when background music is played back. |
| [setBGMVolume](https://intl.cloud.tencent.com/document/product/647/35127#setbgmvolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [setReverbType](https://intl.cloud.tencent.com/document/product/647/35127#setreverbtype) | Sets reverb effect. |
| [setVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35127#setvoicechangertype) | Sets voice changer type. |

### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://intl.cloud.tencent.com/document/product/647/35127#playaudioeffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://intl.cloud.tencent.com/document/product/647/35127#setaudioeffectvolume) | Sets volume level of a single sound effect. |
| [stopAudioEffect](https://intl.cloud.tencent.com/document/product/647/35127#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](https://intl.cloud.tencent.com/document/product/647/35127#stopallaudioeffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://intl.cloud.tencent.com/document/product/647/35127#setallaudioeffectsvolume) | Sets volume level of all sound effects. |


### Network test

| API | Description |
|-----|-----|
| [startSpeedTest](https://intl.cloud.tencent.com/document/product/647/35127#startspeedtest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://intl.cloud.tencent.com/document/product/647/35127#stopspeedtest) | Stops server speed test. |


### MixTranscoding and release to CDN

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35127#setmixtranscodingconfig) | Sets On-Cloud MixTranscoding parameters. |
| [startPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35127#startpublishcdnstream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35127#stoppublishcdnstream) | Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://intl.cloud.tencent.com/document/product/647/35127#getsdkversion) | Gets SDK version information.. |
| [setLogLevel](https://intl.cloud.tencent.com/document/product/647/35127#setloglevel) | Sets log output level. |
| [setConsoleEnabled](https://intl.cloud.tencent.com/document/product/647/35127#setconsoleenabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://intl.cloud.tencent.com/document/product/647/35127#setlogcompressenabled) | Enables or disables local log compression. |
| [setLogDirPath](https://intl.cloud.tencent.com/document/product/647/35127#setlogdirpath) | Modifies log storage path. |
| [setLogListener](https://intl.cloud.tencent.com/document/product/647/35127#setloglistener) | Sets log callback. |
| [showDebugView](https://intl.cloud.tencent.com/document/product/647/35127#showdebugview) | Displays dashboard. |
| [setDebugViewMargin](https://intl.cloud.tencent.com/document/product/647/35127#setdebugviewmargin) | Sets dashboard margin. |
| [callExperimentalAPI](https://intl.cloud.tencent.com/document/product/647/35127#callexperimentalapi) | Calls experimental API. |


### Callback APIs of background music playback

Callback APIs of background music playback.

| API | Description |
|-----|-----|
| [onBGMStart](https://intl.cloud.tencent.com/document/product/647/35127#onbgmstart) | Callback notification of music playback start. |
| [onBGMProgress](https://intl.cloud.tencent.com/document/product/647/35127#onbgmprogress) | Callback notification of music playback progress. |
| [onBGMComplete](https://intl.cloud.tencent.com/document/product/647/35127#onbgmcomplete) | Callback notification of music playback end. |

### Others

| API | Description |
|-----|-----|
| [TRTCViewMargin](https://intl.cloud.tencent.com/document/product/647/35127#trtcviewmargin) | View margin. |

## TRTCCloudListener @ TXLiteAVSDK

Event callback API for TRTC video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](https://intl.cloud.tencent.com/document/product/647/35127#onerror) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://intl.cloud.tencent.com/document/product/647/35127#onwarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://intl.cloud.tencent.com/document/product/647/35127#onenterroom) | Callback of room entry. |
| [onExitRoom](https://intl.cloud.tencent.com/document/product/647/35127#onexitroom) | Callback of room exit. |
| [onSwitchRole](https://intl.cloud.tencent.com/document/product/647/35127#onswitchrole) | Callback of role switching. |
| [onConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35127#onconnectotherroom) | Callback of the result of requesting cross-room call (anchor competition). |
| [onDisConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35127#ondisconnectotherroom) | Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://intl.cloud.tencent.com/document/product/647/35127#onremoteuserenterroom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://intl.cloud.tencent.com/document/product/647/35127#onremoteuserleaveroom) | A user exits the current room. |
| [onUserVideoAvailable](https://intl.cloud.tencent.com/document/product/647/35127#onuservideoavailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://intl.cloud.tencent.com/document/product/647/35127#onusersubstreamavailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://intl.cloud.tencent.com/document/product/647/35127#onuseraudioavailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://intl.cloud.tencent.com/document/product/647/35127#onfirstvideoframe) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onfirstaudioframe) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://intl.cloud.tencent.com/document/product/647/35127#onsendfirstlocalvideoframe) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onsendfirstlocalaudioframe) | The first local audio frame data has been sent. |
| [onUserEnter](https://intl.cloud.tencent.com/document/product/647/35127#onuserenter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://intl.cloud.tencent.com/document/product/647/35127#onuserexit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://intl.cloud.tencent.com/document/product/647/35127#onnetworkquality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://intl.cloud.tencent.com/document/product/647/35127#onstatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://intl.cloud.tencent.com/document/product/647/35127#onconnectionlost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://intl.cloud.tencent.com/document/product/647/35127#ontrytoreconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://intl.cloud.tencent.com/document/product/647/35127#onconnectionrecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://intl.cloud.tencent.com/document/product/647/35127#onspeedtest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://intl.cloud.tencent.com/document/product/647/35127#oncameradidready) | Camera is ready. |
| [onMicDidReady](https://intl.cloud.tencent.com/document/product/647/35127#onmicdidready) | Mic is ready. |
| [onAudioRouteChanged](https://intl.cloud.tencent.com/document/product/647/35127#onaudioroutechanged) | Audio routing changes, i.e., whether the audio is output by speaker or receiver. |
| [onUserVoiceVolume](https://intl.cloud.tencent.com/document/product/647/35127#onuservoicevolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35127#onrecvcustomcmdmsg) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35127#onmisscustomcmdmsg) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://intl.cloud.tencent.com/document/product/647/35127#onrecvseimsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35127#onstartpublishcdnstream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35127#onstoppublishcdnstream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35127#onsetmixtranscodingconfig) | Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35127#trtccloud). |

### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35127#onaudioeffectfinished) | Callback of ending an audio effect. |

### Custom video data frame rendering callbacks
Redirect to [TRTCVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcvideorenderlistener)

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://intl.cloud.tencent.com/document/product/647/35127#onrendervideoframe) | Callback of custom video rendering. |


### Custom audio data frame processing callbacks (read only)
Redirect to [TRTCAudioFrameListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcaudioframelistener)

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#oncapturedaudioframe) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onplayaudioframe) | Audio data from each remote user before audio mixing (for example, if you want to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing). |
| [onMixedPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onmixedplayaudioframe) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
Redirect to [TRTCLogListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcloglistener)

It is recommended to set the callback object in a class that is initialized early, e.g., `Application`.

| API | Description |
|-----|-----|
| [onLog](https://intl.cloud.tencent.com/document/product/647/35127#onlog) | Callback of log printing. |


## Definitions of Key Classes
| API | Description |
|-----|-----|
| [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35129#trtcparams) | Room entry parameters. |
| [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoencparam) | Encoding parameters. |
| [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcnetworkqosparam) | Network bandwidth limit parameters. |
| [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35129#trtcquality) | Video (or network) quality. |
| [TRTCTexture](https://intl.cloud.tencent.com/document/product/647/35129#trtctexture) | Video texture data, including texture ID and EGL environment. |
| [TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoframe) | Video frame information. |
| [TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudioframe) | Audio frame data. |
| [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35129#trtcvolumeinfo) | Volume level. |
| [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35129#trtcspeedtestresult) | Network speed test result. |
| [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35129#trtcmixuser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35129#trtctranscodingconfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcpublishcdnparam) | relayed push parameters. |
| [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudiorecordingparams) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudioeffectparam) | Sound effect. |
| [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35129#trtcstatistics) | Statistics. |
| [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35129#trtcremotestatistics) | Remote audio/video statistics. |
| [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35129#trtclocalstatistics) | Local audio/video statistics. |
