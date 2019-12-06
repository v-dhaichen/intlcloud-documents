## Known Issues
If you use multiple Tencent Cloud services such as CVM, VPC, and TencentDB that are managed by different users sharing your Tencent Cloud account key, you may face the following problems:
- Your key is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permissions of other users, which poses a security risk due to potential misoperations.

## Solution
You can allow different users to manage different services through sub-accounts so as to avoid the above problems. By default, a sub-account doesn't have permission to use a Tencent Cloud service or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603).

If you do not need to manage the access permissions to TencentDB resources for sub-accounts, you can skip this chapter. This will not affect your understanding and usage of other parts in the documentation.

### Getting started
A CAM policy must authorize or deny the use of one or more MongoDB operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

>
> - You are recommended to manage MongoDB resources and authorize MongoDB operations through CAM policies. Although the experience stays the same for existing users who are granted permissions by project, it is not recommended to continue managing resources and authorizing operations in a project-based manner.
>- Effectiveness conditions cannot be set for MongoDB for the time being.

| Relevant Information         | Link                                                         |
| ---------------- | ------------------------------------------------------------ |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/240/32841#yufa) |
| Operation definition in a policy | [MongoDB Operations](https://intl.cloud.tencent.com/document/product/240/32841#caozuo) |
| Resource definition in a policy | [MongoDB Resource Path](https://intl.cloud.tencent.com/document/product/240/32841#lujing) |
| Resource-level permissions | [Resource-level Permissions Supported by MongoDB](https://intl.cloud.tencent.com/document/product/240/32841) |

