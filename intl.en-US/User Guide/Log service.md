---
keyword: [edge log service, Link IoT Edge log service]
---

# Log service

Link IoT Edge log service is integrated with Alibaba Cloud Log Service to provide the log management feature at the edge. If you enable this feature, logs at the edge are automatically synchronized to the cloud and displayed in different levels.

Link IoT Edge log service is based on Alibaba Cloud [Log Service](/intl.en-US/Product Introduction/What is Log Service?.md). If the free quota for Log Service is exceeded, you are charged for the exceeded amount. Before you use this service, we recommend that you familiarize yourself with [t13014.dita\#concept\_y3m\_g5n\_vdb](/intl.en-US/Pricing/Pay-as-you-go.md).

## Prerequisites

An edge instance is created based on the [Build environments](/intl.en-US/User Guide/Set up environments/Link IoT Edge Pro Edition/Install Link IoT Edge on Ubuntu 16.04.md) topic and a RAM role is attached to the edge instance based on the [Access resources of other Alibaba Cloud services](/intl.en-US/User Guide/Access resources of other Alibaba Cloud services.md) topic.

## Procedure

1.  In the left-side navigation pane of the [IoT Platform console](http://iot.console.aliyun.com/), choose **Link IoT Edge** \> **Edge Instances**. Find the created edge instance and click **View**.

2.  Optional. If you are using Log Service the first time, you must activate Log Service. If Log Service has been activated, skip this step.

    1.  On the Instance Details page, click the **Log Service** tab. On this tab, click **Activate Now**.

        On the page that appears, click **Activate Log Service**.

    2.  On the **Activate Log Service** page, read the terms, select I have read and agree, and click **Activate Now**.

    3.  Go to the [IoT Platform console](http://iot.console.aliyun.com/). On the Instance Details page, click the Settings tab. Attach the **AliyunLogFullAccess** RAM policy to the edge instance. For more information about how to attach a RAM policy, see [Access resources of other Alibaba Cloud services](/intl.en-US/User Guide/Access resources of other Alibaba Cloud services.md).

    4.  On the Instance Details page, click the **Log Service** tab. On this tab, turn on the **Enabled** switch.

        ![The Enabled switch](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9647789851/p74151.png)

3.  On the Instance Details page, click the **Log Service** tab. On this tab, click **Log Storage Policies** to configure logging policies.

    Logs at the edge are stored in Log Service. If you specify a longer log retention period, the more storage space is required. Configure the log retention period based on your needs.

    ![Configure logging policies](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9647789851/p32248.png)

    |Parameter|Description|
    |---------|-----------|
    |Log Retention Period|The period for which the gateway log data is retained.|
    |Log Level|The level of the log data to be stored. The priorities of levels are as follows: Error \> Warning \> Information \> Debugging

For example, if you specify Information for the Log Level parameter, log data in the Information, Warning, and Error levels are stored. |

4.  Click **Confirm** to complete the configurations of logging policies.

    After a gateway generates logs, Link IoT Edge filters logs based on specified logging policies and displays logs in the Log Service console.

5.  Optional. You can query logs in Log Service by specifying a log level and time range, and display the results in the Log Service console.


