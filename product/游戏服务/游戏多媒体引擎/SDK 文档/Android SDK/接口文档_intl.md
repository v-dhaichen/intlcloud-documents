## Overview
This article talks about integration for Android in detail to help Android developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME).



## How to Use
### How to use voice chat
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)
### How to convert voice message to text
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)


### Key considerations for using GME

| Important API | Description |
| ------------- |:-------------:|
|Init    		| Initializes GME 	|
|Poll    		| Triggers event callback	|
|EnterRoom	 	| Enters a room  		|
|EnableMic	 	| Enables the microphone 	|
|EnableSpeaker		| Enables the speaker 	|

**Notes:**

**After a GME API is called successfully, QAVError.OK will be returned with a value of 0.**

**GME APIs should be called in the same thread.**

**Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.**

**The Poll API should be called periodically to trigger event callback.**

**Refer to the callback message list for callback information.**

**Device related operations can only be done after entering a room.**

**This document is applicable to GME SDK version：2.3**

## Initialization-related APIs
GME should be initialized with the authentication data before entering a room.

| API | Description |
| ------------- |:-------------:|
|Init    	|Initializes GME 	| 
|Poll    	|Triggers event callback	|
|Pause   	|Pauses the system	|
|Resume 	|Resumes the system	|
|Uninit    	|Uninitializes GME 	|


### Get a singleton
This API is used to get the "ITMGContext GetInstance" instance when using the voice feature.
#### Function prototype 

```
public static ITMGContext GetInstance(Context context)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| context    | Context | Application's context object |


#### Sample code  

```
import com.tencent.TMG.ITMGContext; 
TMGContext.getInstance(this);
```

### Register callback
With the API class, the Delegate method is used to send callback notifications to your application. Register the callback function to the SDK to receive callback messages.

#### Sample code 
```
private ITMGContext.ITMGDelegate itmgDelegate = null;
```
Override this callback function in the constructor to process callback parameters.

| Parameter | Type | Description |
| ------------- |:-------------:| ------------- |
| type    	|ITMGContext.ITMG_MAIN_EVENT_TYPE 	| Event type in the callback response				|
| data    	| Intent message type 						| Callback message, i.e., the event data |



#### Sample code  
```
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```


Register the callback function to the SDK (before a user enters the room).
#### Function prototype 
```
ITMGContext public int SetTMGDelegate(ITMGDelegate delegate)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| delegate    | ITMGDelegate | SDK callback function |

#### Sample code  
```
TMGContext.GetInstance(this).SetTMGDelegate(itmgDelegate);
```



### Initialize the SDK

For more information on how to obtain parameters, please see [GME Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.

You must initialize the SDK before entering a room.
#### Function prototype 

```
ITMGContext public int Init(String sdkAppId, String openID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | String | The sdkAppId obtained from the Tencent Cloud console |
| openID | String | The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000 |

#### Sample code  

```
ITMGContext.GetInstance(this).Init(sdkAppId, openID);
```


### Trigger event callback

The Poll API should be called periodically to trigger event callback.
#### Function prototype

```
ITMGContext int Poll()
```
#### Sample code
```
ITMGContext.GetInstance(this).Poll();
```


### Pause the system

This API is used to notify the engine for Pause when the system Pause occurs.
#### Function prototype

```
ITMGContext int Pause()
```

### Resume the system
This API is used to notify the engine for Resume when the system Resume occurs.
#### Function prototype

```
ITMGContext  int Resume()
```



### Uninitialize the SDK
This API is used to uninitialize the SDK. Uninitialization is needed when switching accounts.

#### Function prototype 
```
ITMGContext int Uninit()

```
#### Sample code  
```
ITMGContext.GetInstance(this).Uninit();
```

## APIs For Voice Chat Room
After the initialization, API for entering a room should be called before Voice Chat can start.

| API | Description |
| ------------- |:-------------:|
|GenAuthBuffer    	|Generates authentication data |
|EnterRoom   		|Enters a room |
|IsRoomEntered   	|Indicates whether the room is entered successfully |
|ExitRoom 		|Exits the room |
|ChangeRoomType 	|Modifies the audio type of the user's room |
|GetRoomType 		|Obtains the audio type of the user's room |


### Authentication information
AuthBuffer is generated for the purpose of encryption and authentication. For more information about the authentication data, refer to  [GME Key](https://cloud.tencent.com/document/product/607/12218).    
A value of type Byte[] is returned by this API. The room ID parameter for voice message must be set to "null".

> Function prototype
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId    		|int   		| The SdkAppId obtained from the Tencent Cloud console |
| roomId    		|String   		|  Room ID, maximum to 127 characters (The room room ID for voice message must be set to "null") |
| openID    	|String 	| User ID					|
| key    		|string 	| The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) 				|


#### Sample code  
```
import com.tencent.av.sig.AuthBuffer;//Header files
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```

### Join a room
This API is used to enter a room with the generated authentication data, and the ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received as a callback. Microphone and speaker are not enabled by default after a user enters the room.

#### Function prototype

```
ITMGContext public abstract int EnterRoom(String roomId, int roomType, byte[] authBuffer)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId 	|String		|  Room ID. maximum to 127 characters.|
| roomType 	|int		| Audio type of the room |
| authBuffer	|byte[]	| Authentication key				|


- For the room audio type definition, refer to [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample code  

```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

### Callback for entering a room
ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received after a user enters a room, the action of this event should be implemented in the OnEvent function.

#### Sample code  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 // Receive the event of entering the room successfully.
        }
	}

```

### Identify whether the user has entered the room successfully
This API is used to identify whether the user has entered the room, and returns a boolean value.
#### Function prototype  
```
ITMGContext public boolean IsRoomEntered()
```
#### Sample code  
```
ITMGContext.GetInstance(this).IsRoomEntered();
```

### Exit a room
This API is used to exit the current room. It is an asynchronous API. The returned value of AV_OK indicates a successful asynchronous delivery.

>If a user enters the room immediately after exiting a room in the application, the developer does not have to wait for the RoomExitComplete notification as a callback of ExitRoom in the API call process, but just calls the API directly.

#### Function prototype  
```
ITMGContext public int ExitRoom()
```
#### Sample code  
```
ITMGContext.GetInstance(this).ExitRoom();
```

### Callback for exiting a room
ITMG_MAIN_EVENT_TYPE_EXIT_ROOM message is received after a user exits a room, the action of this event should be implemented in the OnEvent function.
#### Sample code  

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            //Receive the event of exiting the room successfully.
        }
}
```

### Modify the audio type of the user's room
This API is used to modify the audio type of the user's room. A ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE callback event will be sent.
#### Function prototype  
```
IITMGContext TMGRoom public void ChangeRoomType(int nRoomType)
```


| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| nRoomType    | int    | The room type to be switched to. See the API EnterRoom for the audio type definition. |

#### Sample code  
```
ITMGContext.GetInstance(this).GetRoom().ChangeRoomType(nRoomType);
```


### Obtain the audio type of the user's room
This API is used to obtain the audio type of the user's room. The returned value is the audio type of the room. Returned value of 0 means an error occurred. The audio type definition can be found in the API EnterRoom.

#### Function prototype  
```
IITMGContext TMGRoom public  int GetRoomType()
```

#### Sample code  
```
ITMGContext.GetInstance(this).GetRoom().GetRoomType();
```


### Callback after the room type is set
ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE message is received after a user change the room type. The returned parameters include result, error_info, and new_room_type. new_room_type represents the following information and the action of each event should be implemented in the OnEvent function.

| Event Sub-type | Parameters | Description |
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	|Indicates that the audio type is inconsistent with that of the room to be entered and it is changed to that of the room.	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	|Indicates that the room is entered and the audio type starts changing (e.g., the audio type is changed after the ChangeRoomType API is called.) |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	|Indicates that the room is entered and the audio type has changed |
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	|Indicates that a room member calls the ChangeRoomType API to request a change in the audio type |	


#### Sample code  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//Send a callback after the room type has been changed
	 }
}
```

### Member status change
Notification about this event is sent only when the member status changes. To obtain the member status in real time, cache the notification when receiving it at a higher layer. The event message ITMG_MAIN_EVNET_TYPE_USER_UPDATE is returned. The "data" includes event_id and user_list, and the action of event_id should be implemented in the OnEvent function.
These events will only be sent when exceeding a certain threshold. For example, when audio data of a user is not received for more than two seconds, the ITMG_EVENT_ID_USER_NO_AUDIO will be sent.

|event_id     | Description | What is maintained at the App side |
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|A member enters the room			| Member list		|
|ITMG_EVENT_ID_USER_EXIT    				|A member exits the room			| Member list		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|A member sends audio packages		| Chat member list	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|A member stops sending audio packages		| Chat member list	|

#### Sample code  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE == type)
        {
		//Update member status
		int nEventID = data.getIntExtra("event_id", 0);
		String[] identifierList =data.getStringArrayExtra("user_list");
		 switch (nEventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //A member enters the room
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //A member exits the room
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //A member sends audio packets
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //A member stops sending audio packets
			    break;
		    default:
			    break;
 		    }
	}
}
```
### Quality monitoring events
The message for quality monitoring event is ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY. The returned parameters include weight, floss, and delay, which represent the following information and the action of this event should be implemented in the OnEvent function.

| Parameter | Description |
| ------------- |-------------|
|weight    				| Its value ranges from 1 to 5. The value of 5 indicates excellent quality of audio packets, and the value of 1 indicates poor quality of audio packets, which can barely be used; and "0" represents an initial value and is meaningless. |
|floss    				| Packet loss |
|delay    		| Voice chat delay (ms) |




### Message details

| Message | Description of message |   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       |Enters the room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	|Exits the room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       |Room disconnection due to network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				|Room type change event |

### Details of Data corresponding to the message
| Message | Data         | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|



## Audio APIs for Voice Chat
The APIs for Voice Chat can only be called after the SDK is initialized and you are in the room.
We recommend the following methods when enabling/disabling the microphone or speaker in the user interface:
- For most game apps, call EnableMic and EnableSpeaker APIs. Because calling EnableMic is equivalent to calling EnableAudioCaptureDevice and EnableAudioSend at the same time, and calling EnableSpeaker is equivalent to calling EnableAudioPlayDevice and EnableAudioRecv at the same time.

- For other mobile apps such as social networking apps, enabling/disabling a capturing device will restart both the capturing and the playback devices. If the App is playing background music, it will also be interrupted. But if the microphone is enabled/disabled through control of upstream/downstream, playback will not be interrupted. So the calling method is: Call EnableAudioCaptureDevice(true) and EnableAudioPlayDevice(true) once after entering the room, and call EnableAudioSend/Recv to send/receive audio streams when the microphone button is clicked to enable or disable.

If you wish to release the capture or the playback device separately, please refer to the EnableAudioCaptureDevice and EnableAudioPlayDevice API. Call Pause to pause the audio engine and Resume to resume the audio engine.

### How to call social networking Apps
![](https://main.qcloudimg.com/raw/98ebd91c4df8f5137f6a739a614a5e83.png)


| API | Description |
| ------------- |:-------------:|
|EnableMic    						|Enables/disables the microphone |
|GetMicState    						|Obtains the microphone status |
|EnableAudioCaptureDevice    		|Enables audio capture device		|
|IsAudioCaptureDeviceEnabled    	|Indicates if audio capture device is enabled or not	|
|EnableAudioSend    				|Enables the audio sending 	|
|IsAudioSendEnabled    				|Indicates if audio is being sent or not	|
|GetMicLevel    						|Obtains real-time microphone volume |
|SetMicVolume    					|Sets microphone volume |
|GetMicVolume    					|Obtains microphone volume |
|EnableSpeaker    					|Enables/disables the speaker |
|GetSpeakerState    					|Obtains the speaker status |
|EnableAudioPlayDevice    			|Enables audio playback device		|
|IsAudioPlayDeviceEnabled    		|Indicates if audio playback devices is enabled or not	|
|EnableAudioRecv    					|Enables the audio receving	|
|IsAudioRecvEnabled    				|Indicates if audio is being received or not	|
|GetSpeakerLevel    					|Obtains real-time speaker volume |
|SetSpeakerVolume    				|Sets speaker volume |
|GetSpeakerVolume    				|Obtains speaker volume |
|EnableLoopBack    					|Enables/disables in-ear monitoring |





### Enable/disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
#### Function prototype  
```
ITMGContext public void EnableMic(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable the microphone, set this parameter to true, otherwise, set it to false. |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```

### Obtain the microphone status
This API is used to obtain the microphone status. "0" means microphone is disabled, "1" means microphone is enabled.
#### Function prototype  
```
ITMGContext TMGAudioCtrl int GetMicState() 
```
#### Sample code  
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicState();
```

### Enable/disable audio capture device
This API is used to enable/disable the audio capture device. The audio capture device is not enabled by default. 
- API can only be called after the room is entered.The device will disabled automatically after exiting the room.
- For mobile use case, permission is normally asked when enabling the capture device.

#### Function prototype   

```
ITMGContext public int EnableAudioCaptureDevice(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | true means enable，false means disable |

#### Sample code

```
Enable a capturing device
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Obtain the audio capture device status
This API is used to obtain the audio capture device status.
#### Function prototype

```
ITMGContext public boolean IsAudioCaptureDeviceEnabled()
```
#### Sample code

```
bool IsAudioCaptureDevice =ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enable/disable the audio sending

This API is used to enable/disable the audio sending. Enable means sending the captured voice. 

#### Function prototype

```
ITMGContext public int EnableAudioSend(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | true means enable audio sending，false means not |

#### Sample code  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioSend(true);
```

### Obtain status on if captured audio is being sent 
This API is called to obtain the status if captured audio is being sent.
#### Function prototype
```
ITMGContext TMGAudioCtrl boolean IsAudioSendEnabled()
```
#### Sample code  
```
bool IsAudioSend =  =ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioSendEnabled();
```

### Obtain real-time microphone volume
This API is used to obtain real time microphone volume. An int value is returned.
#### Function prototype  
```
ITMGContext TMGAudioCtrl int GetMicLevel() 
```
#### Sample code  
```
int micLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicLevel();
```

### Set software volume for the microphone
This API is used to set software volume for the microphone. The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.
#### Function prototype  
```
ITMGContext TMGAudioCtrl int SetMicVolume(int volume) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume    |int      | Sets the volume, value range: 0 to 200 |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetMicVolume(volume);
```
### Obtain software volume for the microphone
This API is used to obtain the software volume for the microphone. An int value is returned to indicate the software volume for the microphone. Returned value of 101 means SetMicVolume() has not been called.

#### Function prototype  
```
ITMGContext TMGAudioCtrl public int GetMicVolume()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetMicVolume();
```

### Enable/disable the speaker
This API is used to enable/disable the speaker.
EnableSpeaker = EnableAudioPlayDevice + EnableAudioRecv.
#### Function prototype  
```
ITMGContext public void EnableSpeaker(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       | To disable the speaker, set this parameter to false, otherwise, set it to true. |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

### Obtain the speaker status
This API is used to obtain the speaker status. "0" means speaker is disabled, "1" means speaker is enabled, "2" means speaker is currently in use.
#### Function prototype  
```
ITMGContext TMGAudioCtrl public int GetSpeakerState() 
```

#### Sample code  
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerState();
```

### Enable/disable audio playback device
This API is used to enable/disable audio playback device.

#### Function prototype
```
ITMGContext public int EnableAudioPlayDevice(boolean isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean        | true means enable, false means disable |

#### Sample code 
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### Obtain audio playback device status
This API is used to obtain the status of audio playback device.
#### Function prototype

```
ITMGContext public int IsAudioPlayDeviceEnabled()
```
#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enable/disable the audio receiving
This API is used to enable/disable the audio receving. Enable means playing the received voice. 

#### Function prototype  

```
ITMGContext public int EnableAudioRecv(boolean isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | true means enabling the audio receing. false means not|

#### Sample code  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioRecv(true);
```


### Obtain status on if received audio is being played 
This API is called to obtain the status if received audio is being played.
#### Function prototype
```
ITMGContext TMGAudioCtrl public boolean IsAudioRecvEnabled()
```
#### Sample code  
```
bool IsAudioRecv = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioRecvEnabled();
```

### Obtain real-time speaker volume
This API is used to obtain real time speaker volume. An int value is returned to indicate the real-time speaker volume.
#### Function prototype  
```
ITMGContext TMGAudioCtrl public int GetSpeakerLevel() 
```

#### Sample code  
```
int SpeakLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerLevel();
```

### Set software volume for the speaker
This API is used to set the software volume for the speaker.
The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.


#### Function prototype  
```
ITMGContext TMGAudioCtrl public int SetSpeakerVolume(int volume) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume    |int      | Sets the volume, value range: 0 to 200 |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetSpeakerVolume(volume);
```

### Obtain software volume for the speaker
This API is used to obtain the software volume for the speaker. An int value is returned to indicate the software volume for the speaker. Returned value of 101 means SetSpeakerVolume() has not been called.
"Level" indicates the real-time volume, and "Volume" the is software volume for the speaker. The ultimate volume equals to Level*Volume%. For example, if the value for "Level" is 100 and the one for "Volume" is 60, the ultimate volume will be "60".

#### Function prototype  
```
ITMGContext TMGAudioCtrl public int GetSpeakerVolume()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerVolume();
```


### Enable in-ear monitoring
This API is used to enable in-ear monitoring.
#### Function prototype  
```
ITMGContext TMGAudioCtrl public int EnableLoopBack(boolean enable)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable    |boolean         | Specifies whether to enable in-ear monitoring |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableLoopBack(true);
```

## Accompaniment APIs for Voice Chat
| API | Description |
| ------------- |:-------------:|
|StartAccompany    				       |Starts playing back the accompaniment |
|StopAccompany    				   	|Stops playing back the accompaniment |
|IsAccompanyPlayEnd				|Indicates whether the accompaniment is over |
|PauseAccompany    					|Pauses playing back the accompaniment |
|ResumeAccompany					|Resumes playing back the accompaniment |
|SetAccompanyVolume 				|Sets the accompaniment volume |
|GetAccompanyVolume				|Obtains the accompaniment volume |
|SetAccompanyFileCurrentPlayedTimeByMs 				|Sets the playback progress |

### Start playing back the accompaniment
This API is called to play back the accompaniment. Supported formats are M4A, WAV, and MP3. Volume will reset after being called.

#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int StartAccompany(String filePath, boolean loopBack, int loopCount) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath    	|String    	|Path of the accompaniment file	 |
| loopBack  	|boolean    	| Indicates whether to send a mix. This is generally set to true, so that other users can also hear the accompaniment. |
| loopCount	|int    		| Number of loops to be played. Value -1 means an infinite loop. |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,duckerTimeMs);
```

### Callback for accompaniment playback
After the accompaniment is over, the event message ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH is returned, the action of this event should be implemented in OnEvent function.
The passed parameter "intent" includes result and file_path.
#### Sample code  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH == type)
        {
		//Callback for accompaniment playback
	}
}
```

### Stop playing back the accompaniment
This API is used to stop playing back the accompaniment.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int StopAccompany(int duckerTimeMs)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| duckerTimeMs    |int             | Indicates the fading out time |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StopAccompany(duckerTimeMs);
```

### Indicate whether the accompaniment is over
If it is over, "true" is returned. If it is not, "false" is returned.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public boolean IsAccompanyPlayEnd() 
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().IsAccompanyPlayEnd();
```


### Pause playing back the accompaniment
This API is used to pause playing back the accompaniment.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int PauseAccompany()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PauseAccompany();
```


### Resume playing back the accompaniment
This API is used to resume playing back the accompaniment.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int ResumeAccompany()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().ResumeAccompany();
```



### Set the accompaniment volume
This API is used to set the accompaniment volume. Value range: 0-200. Default is 100. A value greater than 100 means volume up, otherwise volume down.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int SetAccompanyVolume(int vol)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol    |int             | Indicates the volume value |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetAccompanyVolume(Volume);
```

### Obtain the volume of the accompaniment
This API is used to get the accompaniment volume.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int GetAccompanyVolume()
```
#### Sample code  
```
string currentVol = "VOL: " + ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetAccompanyVolume();
```

### Obtain the accompaniment playback progress
The following two APIs are used to obtain the accompaniment playback progress. Note: Current/Total = current loop times, Current % Total = current loop playback position.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public long GetAccompanyFileTotalTimeByMs()
ITMGContext TMGAudioEffectCtrl public long GetAccompanyFileCurrentPlayedTimeByMs()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetAccompanyFileTotalTimeByMs();
ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetAccompanyFileCurrentPlayedTimeByMs();
```


### Set the playback progress
This API is used to set the playback progress.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int SetAccompanyFileCurrentPlayedTimeByMs(long time)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| time | long | Indicates the playback progress in milliseconds |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetAccompanyFileCurrentPlayedTimeByMs(time);
```



## Voice Effect APIs for Voice Chat

| API | Description |
| ------------- |:-------------:|
|PlayEffect    		|Plays the sound effect |
|PauseEffect    	|Pauses the sound effect |
|PauseAllEffects	|Pauses all the sound effects |
|ResumeEffect    	|Resumes the sound effect |
|ResumeAllEffects	|Resumes all the sound effects |
|StopEffect 		|Stops the sound effect |
|StopAllEffects		|Stops all the sound effects |
|SetVoiceType 		|Voice changing effects |
|SetKaraokeType     |Sets karaoke effects|
|GetEffectsVolume	|Obtains the volume of sound effects |
|SetEffectsVolume 	|Sets the volume of sound effects |


### Play the sound effect
This API is used to play sound effects. The sound effect ID in the parameter needs to be managed by the App side, uniquely identifying a separate file. The ID is used to control the effect playback. The file supports m4a, wav and mp3.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int PlayEffect(int soundId, String filePath, boolean loop) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |
| filePath | string | Indicates the sound effect file path |
| loop | boolean | Indicates whether to repeat playback |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PlayEffect(soundId,filePath,loop);
```


### Pause the sound effect
This API is used to pause playing back the sound effect.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int PauseEffect(int soundId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId    |int | Indicates the sound effect ID |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PauseEffect(soundId);
```

### Pause all the sound effects
This API is used to pause all the sound effects.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int PauseAllEffects()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PauseAllEffects();
```

### Resume the sound effect
This API is used to resume playing back the sound effect.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int ResumeEffect(int soundId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().ResumeEffect(soundId);
```

### Resume all the sound effects
This API is used to resume all the sound effects.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int ResumeAllEffects()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().ResumeAllEffects();
```

### Stop the sound effect
This API is used to stop the sound effect.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int StopEffect(int soundId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId    |int | Indicates the sound effect ID |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StopEffect(soundId);
```

### Stop all the sound effects
This API is used to stop all the sound effects.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int StopAllEffects()
```


#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StopAllEffects();
```



### Voice changing effects
This API is used to set the voice changing effects.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl  public int setVoiceType(int type);
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| type    |int | Indicates the voice skin |



| Type | Parameter | Description |
| ------------- |-------------|------------- |
|ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|original sound			|
|ITMG_VOICE_TYPE_LOLITA    				|1	|lolita			|
|ITMG_VOICE_TYPE_UNCLE  				|2	|uncle			|
|ITMG_VOICE_TYPE_INTANGIBLE    			|3	|ethereal			|
| ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|		fatty	|
| ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|heavy metal			|
| ITMG_VOICE_TYPE_DIALECT 				|6	|accent			|
| ITMG_VOICE_TYPE_INFLUENZA 				|7	|flu			|
| ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|caged animal			|
| ITMG_VOICE_TYPE_HEAVY_MACHINE		|9	|heavy machine			|
| ITMG_VOICE_TYPE_STRONG_CURRENT		|10	|strong current			|
| ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|kindergarten			|
| ITMG_VOICE_TYPE_HUANG 					|12	|minions			|


#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().setVoiceType(0);
```

### Set Karaoke effect
This API is called to set the Karaoke effect
#### Function prototype   
```
ITMGContext TMGAudioEffectCtrl  public int SetKaraokeType(int type);
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| type    |int                    |the Karaoke effect type|


|Type     | Parameter | Description |
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL 		|0	|Original			|
|ITMG_KARAOKE_TYPE_POP 				|1	|Pop			|
|ITMG_KARAOKE_TYPE_ROCK 			|2	|Rock			|
|ITMG_KARAOKE_TYPE_RB 				|3	|Hip-pop			|
|ITMG_KARAOKE_TYPE_DANCE 			|4	|Dance			|
|ITMG_KARAOKE_TYPE_HEAVEN 			|5	|New Age			|
|ITMG_KARAOKE_TYPE_TTS 				|6	|TTS		|

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetKaraokeType(0);
```

### Obtain the volume of sound effects
This API is used to obtain the volume (linear volume) of the sound effects. A value greater than 100 means volume up, otherwise volume down.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int GetEffectsVolume()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetEffectsVolume();
```

### Set the volume of sound effects
This API is used to set the volume of sound effects.
#### Function prototype  
```
ITMGContext TMGAudioEffectCtrl public int SetEffectsVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume    |int | Indicates the volume value |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetEffectsVolume(Volume);
```
## Offline Voice
| API | Description |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    		| authentication |
|SetMaxMessageLength    |Specifies the maximum length of a voice message |
|StartRecording		|Starts recording |
|StartRecordingWithStreamingRecognition		| Starts streaming speech recognition		|
|StopRecording    	|Stops recording |
|CancelRecording	|Cancels recording |
|UploadRecordedFile 	|Uploads voice files |
|DownloadRecordedFile	|Downloads voice files |
|PlayRecordedFile 	|Plays recorded voice files |
|StopPlayFile		|Stops playing voice files |
|GetFileSize 		|Obtains the size of a voice file |
|GetVoiceFileDuration	|Obtains the duration of a voice file |
|SpeechToText 		|Converts the voice file into text with Speech Recognition |

### Authentication
Do the authentication after the SDK is initialized. Please refer to the previous section on how to generate authBuffer. 
#### Function prototype    
```
ITMGContext TMGPTT public void ApplyPTTAuthbuffer(String authBuffer)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| authBuffer | String | Authentication data |

#### Sample code   
```
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
```

### Specify the maximum length of a voice message
This API is used to specify the maximum length of a voice message,  the maximum duration of which is limited to 60 seconds.
#### Function prototype  
```
ITMGContext TMGPTT public void SetMaxMessageLength(int msTime)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| msTime    |int                    |Indicates the length of a voice message in millisecond |

> Sample code  
```
ITMGContext.GetInstance(this).GetPTT().SetMaxMessageLength(msTime);
```

### Start recording
This API is used to start recording.
#### Function prototype  
```
ITMGContext TMGPTT public void StartRecording(String filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String | Indicates the path for storing the voice file |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().StartRecording(filePath);
```

### Callback for starting recordings
The callback function OnEvent is called after the recording is started. Th event message is ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE is returned, the action of this event should be implemeted in OnEvent function.

#### Sample code  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE == type)
        	{
            		//Send a callback after the recording has started
        	}
}
```

### Enable streaming speech recognition
This API is used to start streaming speech recognition. Texts obtained from voice-to-text conversion will be returned in real time in its callback. 

#### Function prototype 
```
ITMGContext TMGPTT public void StartRecordingWithStreamingRecognition (String filePath,String language)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String | Indicates the path for storing the voice file |
| language | String | Language code, refer to [language reference list](https://github.com/TencentMediaLab/GME/blob/master/GME%20Developer%20Manual/GME%20SpeechToText.md) |

#### Sample code  
```
String  temple = getActivity().getExternalFilesDir(null).getAbsolutePath() + "/test_"+(index++)+".ptt";
ITMGContext.GetInstance(getActivity()).GetPTT().StartRecordingWithStreamingRecognition(temple,"cmn-Hans-CN");
```

### Callback for streaming speech recognition
The callback function OnEvent is called after the recognition is finished. The event message ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.

|Message Name     | Description         |
| ------------- |:-------------:|
| result    	|Error code indicating whether streaming speech recognition is successful			|
| text    		|text obtained from voice-to-text conversion	|
| file_path 	|local path for the recorded voice file		|
| file_id 		|URL for the recorded voice file uploaded to server	|

|Error Code     | Description         |Recommended Action|
| ------------- |:-------------:|:-------------:|
|32775	|Recording is successful but streaming voice to text is failed	|Call the API UploadRecordedFile to upload the recording, and then call the API SpeechToText to perform voice-to-text conversion.
|32777	|Recording and uploading is successful, but streaming voice to text is failed.	|The message returned includes a URL for successful upload. Call the SpeechToText API to perform voice-to-text conversion.

#### Sample code
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE == type)
        	{
            		//Callback for starting streaming recordings
        	}
}
```


### Stop recording
This API is used to stop recording. This is a asynchronous interface. There will be a callback after the recording is stopped. Only when the recording is successful can the recorded file be used. 
#### Function prototype  
```
ITMGContext TMGPTT public int StopRecording()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().StopRecording();
```

### Cancel recording
This API is used to cancel recording. There will not be a callback after the cancellation.
#### Function prototype  
```
ITMGContext TMGPTT public int CancelRecording()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().CancelRecording();
```

### Upload voice files
This API is used to upload voice files.
#### Function prototype  
```
ITMGContext TMGPTT public void UploadRecordedFile(String filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String |Indicates the path of the voice files to be uploaded  |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().UploadRecordedFile(filePath);
```


### Callback for uploading voice files
After the voice file is uploaded, the event message ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.
The passed parameter includes result, file_path and file_id.
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE== type)
       	 {
           	//Callback for uploading voice files
       	 }
}
```


### Download voice files
This API is used to download voice files.
#### Function prototype  
```
ITMGContext TMGPTT public void DownloadRecordedFile(String fileID, String downloadFilePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | String | URL to a file  |
| downloadFilePath | string | Local path for saving the file |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().DownloadRecordedFile(url,path);
```


### Callback for downloading voice files
After the voice file is downloaded, the event message ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.
The passed parameter includes result, file_path and file_id.

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE== type)
        {
            //Downloaded successfully        
	}
}
```



### Play voice files
This API is used to play voice files.
#### Function prototype  
```
ITMGContext TMGPTT public int PlayRecordedFile(String downloadFilePath) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| downloadFilePath | String |Indicates the path of the file to be played |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().PlayRecordedFile(downloadFilePath);
```


### Callback for playing voice files
After the voice file is played back, the event message ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.
The passed parameter includes result and file_path.
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE== type)
       	 	{
			//Callback for playing a voice file 
		}
}
```

### Stop playing voice files
This API is used to stop playing back voice files.
#### Function prototype  
```
ITMGContext TMGPTT public int StopPlayFile()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().StopPlayFile();
```
### Obtain the size of a voice file
This API is used to get the size of a voice file.
#### Function prototype  
```
ITMGContext TMGPTT public int GetFileSize(String filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String | Indicates the path to a voice file |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().GetFileSize(path);
```

### Obtain the length of a voice file
This API is used to obtain the duration of a voice file (in milliseconds).
#### Function prototype  
```
ITMGContext TMGPTT public int GetVoiceFileDuration(String filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String | Indicates the path to a voice file |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().GetVoiceFileDuration(path);
```


### Convert the specified voice file into text with Speech Recognition
This API is used to convert the specified voice file into text with Speech Recognition.

#### Function prototype  
```
ITMGContext TMGPTT public int SpeechToText(String fileID)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | String |  Indicates the URL to a voice file  |

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID);
```

### Convert the specified voice file into text with Speech Recognition(specify language)
This API is used to convert the specified voice file into text with Speech Recognition.
#### Function prototype  
```
ITMGContext TMGPTT public int SpeechToText(String fileID, String language)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID    |char* | Indicates the URL to a voice file |
| language    |char*                     |Language code, refer to [language reference list](https://github.com/TencentMediaLab/GME/blob/master/GME%20Developer%20Manual/GME%20SpeechToText.md)|

#### Sample code  
```
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID,"cmn-Hans-CN");
```

### Callback for Speech Recognition
After the specified voice file is converted into text with Speech Recognition, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE is returned, which is identified in the OnEvent function.
The passed parameter includes result, file_path and text (recognized text).
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE == type)
       	 {
            //Voice file recognized successfully       
	 }
}
```
## Advanced APIs

### Obtain the version number
This API is used to get the SDK version number for analysis.
#### Function prototype
```
ITMGContext public void GetSDKVersion()
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetSDKVersion();
```

### Set the print log level
This API is used to set the print log level.
#### Function prototype
```
ITMGContext int SetLogLevel(int logLevel, bool enableWrite, bool enablePrint)
```



| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| logLevel    		|int | Indicates the print log level |
| enableWrite    	| bool | Indicates whether to write a file. The default is Yes |
| enablePrint    	|bool | Indicates whether to write a console. The default is Yes |




| ITMG_LOG_LEVEL | Description |
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0		| Do not print logs			|
|TMG_LOG_LEVEL_ERROR=1		| Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			| Prints prompt logs		|
|TMG_LOG_LEVEL_DEBUG=3		| Prints development and debugging logs	|
|TMG_LOG_LEVEL_VERBOSE=4		| Prints verbose logs		|
#### Sample code  
```
ITMGContext.GetInstance(this).SetLogLevel(1,true,true);
```



### Set the path of logs to be printed
This API is used to set the path of the log to be printed. The default path is: /sdcard/Android/data/xxx.xxx.xxx/files.
#### Function prototype
```
ITMGContext int SetLogPath(String logDir)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| logDir | String | Path|

#### Sample code  
```
ITMGContext.GetInstance(this).SetLogPath(path);
```


### Obtain diagnostic messages
This API is used to obtain information about the quality of real-time audio/video calls. This API is mainly used to check the quality of real-time calls and troubleshoot problems, and can be ignored for this service.
#### Function prototype  
```
IITMGContext TMGRoom public String GetQualityTips() 
```
#### Sample code  
```
ITMGContext.GetInstance(this).GetRoom().GetQualityTips();
```

### Add an ID to the audio data blacklist
This API is used to add an ID to the audio data blacklist. A return value of 0 indicates that the call is failed.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openId | String |ID that needs to be added to the blacklist |

#### Sample code  

```
ITMGContext.GetInstance(this).GetAudioCtrl().AddAudioBlackList(openId);
```

### Remove an ID from the audio data blacklist
This API is used to remove an ID from the audio data blacklist. A return value of 0 indicates that the call failed.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(String openId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openId | String | ID that needs to be removed from the blacklist|

#### Sample code  

```
ITMGContext.GetInstance(this).GetAudioCtrl().RemoveAudioBlackList(openId);
```


## Callback Messages

#### Message list:

| Message | Description of message |   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		| Enters the audio room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		| Exits the audio room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT		| Room disconnection due to network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE		|Room type change event |
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH		| Indicates that the accompaniment is over			|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE		| Indicates that the room members are updated		|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE	| Indicates that PTT recording is completed			|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE	| Indicates that the PTT is successfully uploaded			|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	| Indicates that the PTT is successfully downloaded			|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		| Indicates that the playback of PTT is completed			|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	| Indicates that the voice-to-text conversion is completed			|

#### Data list

| Message | Data         | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|result; error_info			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"microphone (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|result; error_info 			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"microphone (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; file_path;file_id		|{"file_id":"","filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE	|result; text; file_path;file_id		|{"file_id":"","filepath":","text":"","result":0}|

