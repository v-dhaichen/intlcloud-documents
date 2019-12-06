
>Cost allocation tags is currently in beta . You can contact your sales rep or submit a ticket to try it out.

# Feature Description #

Tags are the labels you assign to Tencent Cloud resources. They can be used for managing resources or grouping costs. Each tag consists of a key and a value. A key can have more than one value.
Tag keys that are set up as cost allocation tags are displayed in the bills as columns. Each key will become an additional column. The tag values that you set up for a tag key for a resource are displayed in rows under the tag key column in the bills. Cost allocation tags can also be used to filter and break down a bill.


# Instructions #

Log in to Tencent Cloud console and enter the tag management page by selecting [**Tag**](https://console.cloud.tencent.com/tag/resources) from the **Products** drop-down menu.

**1. Creating a tag**

Select **Tag List** from the left sidebar to enter the tag list page. You can create tag keys and the corresponding tag values by clicking the **Create** button on the page.

![10176_1](https://main.qcloudimg.com/raw/cb1f2161836a4e59406059dead17f310.png)

You will see your created tag on the page when you are done.

**2. Assigning the tag to a resource**

After creating tags, you can assign them by selecting **Resource Tag** from the left sidebar. Select the resource type and region, click the **Query Resource** button, and you will see a list of the corresponding resources. Select the resource that you want to tag, click **Edit Tag Value** and **Add Tag Key** to tag the resource.
You can also go to the product console to tag resources.

![10176_2](https://main.qcloudimg.com/raw/5ffebb44857771cadd60716f39219b11.png)

**3. Setting up cost allocation tags**

If you want to use the tag feature for your bills, you will need to enter the **Billing Center** and go to **Bills** > [**Cost Allocation Tags** ](https://console.cloud.tencent.com/expense/tag) on the left sidebar. The tag keys set up as cost allocation tags will be displayed as separate columns, and you can use them to filter and break down the bills.
You can see the list of tag keys that have been created on this page. Select a tag key and click on **Set as Cost Allocation Tag** to set the tag key as the cost allocation tag. Similarly, you can select a tag key and click **Cancel Cost Allocation Tag** to cancel the cost allocation tag.

![10176_3](https://main.qcloudimg.com/raw/59dfc9eced779b0539878e1a90956c30.png)

Note: You can set a maximum of 5 cost allocation tags. We recommend that you only select one tag key to be the cost allocation tag. Keeping the number of cost allocation tags low makes it easier for cost management.

# Using Tags #

If you have enabled the tag feature and set up cost allocation tags, you will see the tags in the bills. Tags will appear in the bills starting from the month cost allocation tag is first set up.

**Note:** No changes will be made to bill data and contents for months that have already been billed before setup. These bills will not include tags.

**Tags in the Console**

1. Bill overview

You will see the new **By Tag** option the [Bill Overview](https://console.cloud.tencent.com/expense/bill/overview) page.After clicking to enter,you can select at a  tag key to see the
bar chart and list of the related resources.

![10176_4_2](https://main.qcloudimg.com/raw/41b6a410109605367d171775c21c3931.png)

2. Bill by Instance and Bill Details

The table on Bill by Instance and Bill Details under Billing Details include columns of all tag keys set up as cost allocation tags.
These columns are titled with the format “Tag Key: XXX”. You can filter the bill by these tags.

![10176_5](https://main.qcloudimg.com/raw/83f5006a6442d7f5a6b42d893fbacd8a.png)

**Tags in Bill Files**

If you have enabled the tag feature and set up cost allocation tags, you will see tags in the downloaded bill files of varying levels. You can use tag keys to filter tables in the files.

1. Tags in L2-level bill files (summarized by resource ID)

In a bill file summarized by resource ID, you can see the tag key columns and the corresponding tag values on the rows under each column on the right side of the table (the tag value will be blank if you have not set up the tag value for this tag key for the resources of a certain row).

Note: A resource ID with different tag values is displayed in multiple rows, while those with one tag value are displayed in the same row.

![10176_6](https://main.qcloudimg.com/raw/30979ceca9e19901a33da6d69b6ad88b.png)

2. Tags in L3-level bill files (bill details)

In a bill details file, you can see the tag key columns and the corresponding tag values on the rows under each column on the right side of the table (the tag value will be blank if you have not set up the tag value of this tag key for the resources of a certain row).

![10176_7](https://main.qcloudimg.com/raw/cb9611604c904f825b40c207c76a0f7f.png)




