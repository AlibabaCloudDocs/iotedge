# GetEdgeInstance

Queries detailed information about an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=GetEdgeInstance&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetEdgeInstance|The operation that you want to perform. Set the value to GetEdgeInstance. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance whose detailed information you want to query and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|BizEnable|Boolean|true|Indicates whether the edge instance was enabled. Valid values:

-   true: enabled
-   false: disabled |
|GmtCreate|String|2019-06-26 12:33:25|The time when the edge instance was created. |
|GmtCreateTimestamp|Long|1581912859713|The UNIX timestamp when the edge instance was created. |
|GmtModified|String|2019-06-26 12:33:25|The last time when the edge instance was updated. |
|GmtModifiedTimestamp|Long|1581912859713|The last UNIX timestamp when the edge instance was updated. |
|InstanceId|String|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. |
|LatestDeploymentStatus|Integer|2|The status of the latest deployment task. Valid values:

-   0: The task was not started.
-   1: The task was being processed.
-   2: The task was successful.
-   3: The task failed. |
|LatestDeploymentType|String|deploy|The type of the latest deployment task. Valid values:

-   deploy: deploys the edge instance.
-   reset: resets the edge instance. |
|Name|String|Test instance new|The name of the edge instance. |
|RoleArn|String|acs:ram::1473922805\*\*\*\*\*\*:role/aliyuniotaccessingfcrole|The Alibaba Cloud Resource Name \(ARN\) of the RAM role. |
|RoleAttachTime|String|2020-02-19 11:25:48|The time when the RAM role was attached to IoT Platform. |
|RoleAttachTimestamp|Long|1581912859713|The UNIX timestamp when the RAM role was attached to IoT Platform. |
|RoleName|String|AliyunIOTAccessingFCRole|The name of the RAM role. |
|Spec|Integer|30|The specifications of the edge instance. Valid values:

-   10: Lite Edition
-   20: Standard Edition
-   30: Pro Edition |
|Tags|String|k1:v1,k2:v2|The tags of the edge instance. Each tag is a `key-value` pair. Multiple tags are separated with commas\(,\). Example: `k1:v1,k2:v2`. |
|Type|String|0|Indicates whether you own the edge instance or you are authorized to use the edge instance. Valid values:

-   0: You own the edge instance.
-   1: You are authorized to use the edge instance. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|16645053-546B-4D7C-832E-E519B0E23CF1|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=GetEdgeInstance
&InstanceId=F3APY0tPLhmgGtx0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetEdgeInstanceResponse>
    <RequestId>16645053-546B-4D7C-832E-E519B0E23CF1</RequestId>
    <Data>
        <GmtCreate>2019-06-26 12:33:25</GmtCreate>
        <BizEnable>true</BizEnable>
        <InstanceId>F3APY0tPLhmgGtx0****</InstanceId>
        <LatestDeploymentType>deploy</LatestDeploymentType>
        <GmtModified>2019-06-26 16:16:22</GmtModified>
        <Spec>30</Spec>
        <Tags>k1:v1,k2:v2</Tags>
        <Name>Test instance new</Name>
        <LatestDeploymentStatus>2</LatestDeploymentStatus>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</GetEdgeInstanceResponse>
```

`JSON` format

```
{
  "RequestId": "16645053-546B-4D7C-832E-E519B0E23CF1",
  "Data": {
    "GmtCreate": "2019-06-26 12:33:25",
    "BizEnable": true,
    "InstanceId": "F3APY0tPLhmgGtx0****",
    "LatestDeploymentType": "deploy",
    "GmtModified": "2019-06-26 16:16:22",
    "Spec": 30,
    "Tags": "k1:v1,k2:v2",
    "Name": "Test instance new",
    "LatestDeploymentStatus": 2
  },
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

