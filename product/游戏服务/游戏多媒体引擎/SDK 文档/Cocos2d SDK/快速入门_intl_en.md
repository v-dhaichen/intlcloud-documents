This document helps Cocos2D developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME). 


This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15218).


| Important API | Description |
| ------------- |:-------------:|
| Init | Initializes GME |
| Poll | Triggers event callback |
| EnterRoom | Enters a room |
| EnableMic | Enables the microphone |
| EnableSpeaker | Enables the speaker |

>**Notes:**
- Configure the project before using GME, otherwise the SDK is not valid.
- After a GME API is called successfully, QAVError.OK will be returned with a value of 0.
- GME APIs should be called in the same thread.
- Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.
- The Poll API should be called periodically to trigger event callback.
- Refer to the callback message list for callback information.
- Device related operations can only be done after entering a room.
- For error code details, please see [Error Codes](https://cloud.tencent.com/document/product/607/15173).


## Integration Directions
### 1. Get a singleton
To use the voice feature, get the ITMGContext object first.

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2. Initialize the SDK
For more information on getting parameters, see [Integration Guide](https://cloud.tencent.com/document/product/607/10782).
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.
You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext virtual void Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | char* | The SdkAppId obtained from the Tencent Cloud Console |
| openID | char* | The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000. |

#### Sample code 
```
#define SDKAPPID3RD "1400035750"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### 3. Trigger event callback
The Poll API should be called periodically to trigger event callback.
#### Function prototype

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}
```
#### Sample code
```
ITMGContextGetInstance()->Poll();
```


### 4. Authentication information

This API is used to generate AuthBuffer for encryption and authentication. For more information on deployment at the backend, see [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).  
To obtain authentication for voice message, enter "null" for the room ID parameter.

#### Function prototype
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| dwSdkAppID | int | The sdkAppID obtained from the Tencent Cloud Console |
| strRoomID | char*  | Room ID, which is limited to 127 characters (The room ID parameter for voice message must be set to null.) |
| strOpenID | char*    | User ID |
| strKey | char* | The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) |
| strAuthBuffer | char* | Returned authbuff |
| bufferLength | int   | Length of passed authbuff. 500 is recommended. |



#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```

### 5. Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM.  
- By default, Microphone and speaker will not be enabled after you enter the room.
- The API Init should be called before the API EnterRoom.

#### Function prototype
```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//common EnterRoom API
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | char* | Room ID, which is limited to 127 characters |
| roomType | ITMG_ROOM_TYPE | Audio type of the room |
| authBuffer | char* | Authentication key |
| buffLen | int | Length of the authentication key |

For more information on room's audio types, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 6. Callback for entering a room
The ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is returned after a user enters a room, which is checked in the OnEvent function.

#### Sample code 

```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
		}
	}
}
```

### 6. Enable/Disable the microphone
This API is used to enable/disable the microphone. By default, the microphone and speaker will not be enabled after a user enters a room.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| bEnabled | bool | To enable the microphone, set this parameter to true, otherwise set it to false. |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 7. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | bool | To disable the speaker, set this parameter to false, otherwise set it to true. |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```



