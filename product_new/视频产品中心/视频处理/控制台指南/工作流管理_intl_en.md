## Introduction
When you set up a workflow, videos uploaded to the specified bucket and directory will automatically be processed accordingly, and the output videos will be uploaded to the specified bucket and directory. Workflows can be configured to include tasks such as transcoding, screencapturing, animated image generating, and watermarking.

## Creating a Workflow
1. Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Workflow Management** on the left sidebar.
2. Click **Create Workflow** to enter the workflow creation page and set the workflow name, trigger bucket, trigger directory, output bucket, output directory, event notification and configuration items.
![](https://main.qcloudimg.com/raw/314b57f24a325fc3f4a3f4da16594006.png)
	- **Workflow name**
	This field is required and can contain up to 128 letters, digits, and underscores (_). The workflow name must be unique.
	- **Trigger bucket**
		- This field is required. You can select a bucket created under the current APPID as the trigger bucket.
		- When a workflow is enabled, video files uploaded to this bucket will automatically trigger execution of the workflow.
	- **Trigger directory**
	This field is optional and must end with a slash (/). If it is left blank, the workflow will take effect for all directories in the trigger bucket.
	- **Output bucket**
		- This field is required and will be the same as the trigger bucket by default. You can select a bucket under the current APPID in the same region as the trigger bucket as the output bucket.
		- After a workflow is completed, the output video file will be stored in this bucket.
	- **Output directory**
	This field is optional and must end with a slash (/). If it is left blank, the output directory will be the same as the triggered directory.
	- **Event notification**
		- Event notifications are disabled by default. When enabled, you can select the queue model or topic model in CMQ model settings and set the model name and region. MPS event notifications will then be sent to the specified CMQ queue or topic.
		- Event notification to CMQ is available only after you activate the CMQ service and create a queue model or topic model. For more information, please see [CMQ](https://intl.cloud.tencent.com/document/product/406/8435).
	- **Configuration items**
	Available tasks include transcoding, screencapturing, or animated image generating. You must select at least one for the workflow. For more information, please see [Task Configuration Description](#p1).

<span id = "p1"></span>**Task Configuration Description**

Task Category | Support Preset or Custom Templates | Supported Templates
-|-|-
 Transcoding task | Transcoding template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Transcoding template: Select from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates do not meet your needs, select [Template Settings > Transcoding Template](https://intl.cloud.tencent.com/document/product/1041/33486#video-transcoding-template) to create a custom template. <br><li>Watermarking template: Up to four watermarks can be added to one transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermarking Template](https://intl.cloud.tencent.com/document/product/1041/33486#watermarking-template) to create a custom template.
 Screencapturing task | Screencapturing template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Screencapturing template: There are three types of screenshots, namely, time point screenshot, sampled screenshot, and image sprite screenshot. You must select the matching template for each screenshot type. You need to select the time points for time point screenshots. If the existing templates do not meet your needs, select [Template Settings > Screencapturing Template](https://intl.cloud.tencent.com/document/product/1041/33486#time-point-screenshot) to create a custom template. <br><li>Watermarking template: Up to four watermarks can be added to one transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermarking Template](https://intl.cloud.tencent.com/document/product/1041/33486#watermarking-template) to create a custom template.
Animated image generating task | Animated image generating template: <li>Preset templates are supported <br><li>Custom templates are supported | Animated image generating template: You can add multiple animated image generating templates. The duration of the animated image can be reconfigured. If the existing templates do not meet your needs, select [Template Settings > Animated Image Generating Template](https://intl.cloud.tencent.com/document/product/1041/33486#animated-image-generating-template) to create a custom template.



## Managing a Workflow

1. Log in to the [MPS Console](https://console.cloud.tencent.com/vod) and click **Workflow Management** on the left sidebar.
2. The workflow list displays information such as the workflow name, trigger bucket, region, directory, creation time, and enablement status. You can sort workflows by creation time, search for a workflow by name, and view, edit, or delete a specified workflow.
	-  **Enable a workflow**
		- Workflows are disabled by default. Click the status button of a workflow to enable it.
		- Uploaded videos in the trigger bucket will auto-trigger workflow execution only when the workflow is enabled.
	- **Disable a workflow**
		- Click the status button of a workflow to disable it.
		- After the workflow is disabled, videos uploaded to the trigger bucket will not trigger automatic execution of video processing tasks.
	- **Edit a workflow**
		- Click **Edit** in the "Operation" column of the target workflow to edit the workflow. You can edit the workflow name, trigger bucket, trigger directory, output bucket, output directory, event notification, and configuration items.
		- You cannot edit or delete an enabled workflow.
	- **Delete a workflow**
		- Click **Delete** in the "Operation" column of the target workflow to delete it.
		- After the workflow is deleted, videos uploaded to the trigger bucket will not trigger automatic execution of video processing tasks.
		- You cannot edit or delete an enabled workflow.

