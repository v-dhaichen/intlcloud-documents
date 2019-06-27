[//]: # (chinagitpath:XXXXX)

## Preparations
- Developers need to complete the following steps when integrating the security SDK:
 1. Copy the SDK dynamic library to the specified project directory associated with the game platform and the CPU architecture.
 2. Call the SDK API based on the game_id and user's login information.
 3. Verify whether the SDK is integrated correctly.

- The following files are required for the integration of the security SDK to Android OS written in C/C++:
```
tp2.cs
tp2.jar (Android)
libtersafe2.so (Android)
```
- Permissions required:
```
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.GET_TASKS" />
<uses-permission android:name="android.permission.INTERNET" />
```
- SDK API functions:
```
Initialization API: Tp2SdkInitEx
User login API: Tp2UserLogin
API for switching between foreground and background: Tp2SetGamestatus
```

## Adding SDK Files to the Project
### Add files
1. Move tp2.cs from the sdk\android\c# directory into the project's Assets directory.
2. Move tp2.jar from the sdk\android\c# directory into the project's Assets\Plugins\Android directory.
3. Multi-CPU:
When we use Unity5.0, for example, if the game supports multi-CPU architecture (currently only arm-v7a and x86 are supported) on Android, copy libtersafe2.so in both armeabi and x86 folders under the sdk\android\c#\lib directory to the following directories respectively:
```
Assets/Plugins/Android/libs/armeabi-v7a/
Assets/Plugins/Android/libs/x86/
```
4. Single CPU architecture:
When we use Unity4.5, for example, if the game only supports arm-v7, move tp2.jar provided by SDK and libtersafe2.so from the armeabi-v7a directory to the /Assets/Plugins/Android/ directory.

### Setting of project attributes
If multi-CPU architecture is supported, select "File" -> "Build Settings" -> "Player Settings" -> "Other Settings" -> "Device Filter" -> "FAT(ARMv7+x86)".

![](https://mc.qcloudimg.com/static/img/c94b432701454a02efdc3a2110902fa6/image.png)

## Calling SDK API
### Initialization function
**Function signature**
```
void Tp2SdkInitEx (int gameId, string appKey);
```
**Parameter description**

| Parameter | Required | Description |
|---------|---------|---------|
| gameId | Yes | The game_id assigned by Tencent Cloud |
| appKey | Yes | The game_key assigned by Tencent Cloud, which corresponds to the game_id. |
Both gameID and appKey are automatically generated after a new game has been registered on the Tencent Cloud official website (xxxxxxxxxxxx).
- **Return value**: 0 indicates a successful call.

### Set the user information
**Function signature**
```
void Tp2UserLogin (int accountType, int worldId, String openId, String roleId);
```

**Parameter description**

| Parameter | Title 2 |
|---------|---------|
| account_type | Account type associated to the operating platform. Refer to TssSdkEntryId below. |
| world_id | Information on the server where user's game role is created |
| open_id | User's unique ID, which can be a custom string. This is required for penalties purposes. |
| role_id | Identifies the roles created by a user |

For the account_type, 1 indicates QQ (default), 2 indicates WeChat, and 99 indicates other platforms. Chinese and international mainstream platforms, please refer to the following values.
```
enum TssSdkEntryId
{
ENTRY_ID_QZONE = 1, // QQ
ENTRY_ID_MM = 2, // WeChat
ENTRT_ID_FACEBOOK = 3, // facebook
ENTRY_ID_TWITTER = 4, // twitter
ENTRY_ID_LINE = 5, // line
ENTRY_ID_WHATSAPP = 6, // whatsapp
ENTRY_ID_OTHERS = 99, // Other platforms
};
```
- world_id is defined by the game. Enter 0 if the game has only one server.
- role_id is used to identify different roles of an account under one server. Enter "" if there is only one role.
- open_id is assigned by the specific operating platform to uniquely identify users.
- **Return value**: 0 indicates a successful call.

### Set the game status
**Function signature**
```
void Tp2SetGamestatus (Tp2Status status);
```
**Parameter description**

| Parameter | Description |
|---------|---------|
| status | Foreground Tp2Status. FRONTEND<br>Background Tp2Status. BACKEND |

**Enumeration types**
```
public enum Tp2Status
{
FRONTEND = 1, // Foreground
BACKEND = 2 // Background
}
```
**Return value**: 0 indicates a successful call.

### When to call the function
1. Call Tp2SdkInitEx immediately after the game is launched. Parameters are gameID and appKey. Calling the security API function earlier can better protect the game process.
2. Tp2UserLogin is called after the game is authorized by the user to access its login information. If the game has set world_id and role_id, then call the Tp2UserLogin function after obtaining both world_id and role_id. During gameplay, if you need to retrieve the user's login information in situations like when the network is disconnected or the user logged out and needs to re-login, you will need to call the function again. The parameter to be passed is the user's account information, which can be customized.
3. Tp2SetGamestatus is called when the game switches between foreground to background. When the game switches from background to foreground, the parameter is set to Tp2Status. FRONTEND, and when the game switches from foreground to background, the parameter is set to Tp2Status. BACKEND. Some of the SDK functions stop running when the game switches to background, so the API may affect the normal running of SDK functions.

### Sample Code
```
void Awake ()
{
Tp2Sdk.Tp2SdkInitEx(8888, "d5ab8dc7ef67ca92e41d730982c5c602");
}
// Called after the user logs in
void Start ()
{
int accountType = (int)Tp2Entry.ENTRY_ID_QZONE ; /* Account type */
int worldId = 100; /* Server id*/
string openId = "B73B36366565F9E02C752"; /* User id*/
string roleId = "paladin"; /* Role id*/
Tp2Sdk.Tp2UerLogin(accountType, worldId, openId, roleId);
}
// Called when the game switches between foreground and background
void OnApplicationPause (bool pause)
 {
if (pause)
 {
Tp2Sdk.Tp2SetGamestatus(Tp2Status. BACKEND); // Switching to background
}
else
{
Tp2Sdk.Tp2SetGamestatus(Tp2Status. FRONTEND); // Switching to foreground
}
}
```

## Verifying Whether the SDK is Integrated Correctly
1. Connect your Android phone to a Windows PC via a USB cable. After the connection is successful, log in to the Android ADB console using Windows CMD, as shown below:

 ![](https://mc.qcloudimg.com/static/img/091f2d44b4862e843748fdd9655e9914/image.png)
 
2. Type cd /sdcard, press enter, then type mkdir sdk, and press enter, to create the /sdcard/sdk directory. If the directory already exists, a prompt indicating "mkdir failed for /sdcard/sdk. File exists" will appear, and you can proceed to the next step:

 ![](https://mc.qcloudimg.com/static/img/748c74c2ef3f5bec2a650f3d8eb0bdc6/image.png)
 
3. Type cd /sdcard/sdk to enter the directory, and type echo>enable.log to create an empty file enable.log:

 ![](https://mc.qcloudimg.com/static/img/26aa6733a77a4c2625d131cddba47b89/image.png)
 
Files under the directory created by the shell may not be accessed on some models. In this case, change the /sdcard/sdk directory with root user or use another mobile phone.

 ![](https://mc.qcloudimg.com/static/img/91cd8bb85e88eede943d47570a792c35/image.png)
 
4. Start and log in to the game, check whether tp2.log and tlog.log are generated in the /data/data/log directory, as shown below:

 ![](https://mc.qcloudimg.com/static/img/3ce91cbdb15cdb72998fbfcc2bdf074e/image.png)
 
If no log is generated, check whether you have the read/write permission to /sdcard/sdk and enable.log. This directory cannot be read/written on a small number of models. Use another model for testing or change /sdcard/sdk to /data/data/log with root user.
>**Note:**
>enable.log is only used for testing purposes.
5. Open the tp2.log file, and check whether it contains the information of three native APIs **tp2_sdk_init_ex, tp2_setuserinfo and setgamestatus** as well as the jar packet's version number **jar_ver**. Only when all the above conditions are met, can the security SDK run properly. setgamestatus:1 indicates that the current process is running in the foreground, and setgamestatus:2 indicates that the current process is running in the background.
Verify whether the API is correctly called by switching the App between foreground and background, and also check whether the userinfo is entered correctly.

 ![](https://mc.qcloudimg.com/static/img/75eef4a35cf89e8e1d02be304403377b/image.png)
 
6. Open tlog.log to view the data sent by the security SDK, as shown below:

 ![](https://mc.qcloudimg.com/static/img/50526870e79bb4d21d5b5bb0c333f86f/image.png)
 
In addition to reporting some basic process information during initialization, the security SDK also sends data according to the results of periodic security scanning, such as the incorrect signature of the App certificate, modification of memory data, a running add-on process, etc. The tlog.log records the data (only generated during testing) sent by the SDK. Generally, the data size per hour is about 20 KB. You can check the size of tlog.log to calculate the volume of data sent by the security SDK.

