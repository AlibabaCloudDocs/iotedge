# UpdateEdgeInstance

Updates an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of five queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=UpdateEdgeInstance&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateEdgeInstance|The operation that you want to perform. Set the value to UpdateEdgeInstance. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that you want to update and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|Name|String|Yes|LinkIoTEdge\_Node|The name of the edge instance.

The name can be up to 20 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|Tags|String|No|k1:v1,k2:v2|The tags of the edge instance. Each tag is a key-value pair. Multiple tags are separated with commas \(,\). Example: `k1:v1,k2:v2`.

-   Take note of the following limits on tag keys:
    -   Tag keys cannot be left empty.
    -   Tag keys must be unique in the edge instance.
    -   Tag keys support only letters.
    -   Each tag key can be up to 20 characters in length.
-   Take note of the following limits on tag values:
    -   Tag values cannot be left empty.
    -   A tag value can contain letters, digits, underscores \(\_\), and hyphens \(-\).
    -   Each tag value can be up to 20 characters in length.

If you do not set this parameter, this parameter is not updated. |
|Spec|Integer|No|10|The specifications of the edge instance. Valid values:

-   10: Lite Edition
-   20: Standard Edition
-   30: Pro Edition

If you do not set this parameter, this parameter is not updated. |
|BizEnable|Boolean|No|true|Specifies whether to enable the edge instance. Valid values:

-   true: enables the edge instance.
-   false: disables the edge instance.

If you do not set this parameter, this parameter is not updated. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~135196~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|10CA6DAD-EBAF-4D3E-9309-9DB5B0FF48F2|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=UpdateEdgeInstance
&InstanceId=F3APY0tPLhmgGtx0****
&Spec=30
&Tags=room:1,floor:1
&BizEnable=true
&Name=Test instance new
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateEdgeInstanceResponse>
      <RequestId>10CA6DAD-EBAF-4D3E-9309-9DB5B0FF48F2</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</UpdateEdgeInstanceResponse>
```

`JSON` format

```
{
  "RequestId": "10CA6DAD-EBAF-4D3E-9309-9DB5B0FF48F2",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

