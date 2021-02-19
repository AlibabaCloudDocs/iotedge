# BatchUnbindDeviceFromEdgeInstance

Unbinds multiple devices from the edge instance.

## Limits

A single Alibaba Cloud account can run a maximum of 5 queries per second \(QPS\).

**Note:** RAM users share the quota of the Alibaba Cloud account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BatchUnbindDeviceFromEdgeInstance&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchUnbindDeviceFromEdgeInstance|The operation that you want to perform. Set the value to BatchUnbindDeviceFromEdgeInstance. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. |
|IotIds.N|RepeatList|Yes|BXPV9Ks3bxwM9fD\*\*\*\*0000101|The IDs of devices. You can call the [t7584.md\#](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDevice.md) operation to query detailed information of all devices under the current Alibaba Cloud account and retrieve the required device IDs.

**Note:** You can specify a maximum of 20 devices when calling the BatchUnbindDeviceFromEdgeInstance operation. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for public instances. However, this parameter is required for the instances that you have purchased. |

In addition to the preceding exclusive request parameters, you must specify common request parameters when calling this API operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|34755DC3-2809-4AE2-BAD8-7B81ED69D570|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. true: indicates that the call was successful. false: indicates that the call failed. |
|Code|String|Success|The error code. Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message returned if the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=BatchUnbindDeviceFromEdgeInstance
&IotIds.2=BXPV9Ks3bxwM9fD****0000101
&IotIds.1=sjI0Sd124XFYyjBY****000101
&InstanceId=F3APY0tPLhmgGtx0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchUnbindDeviceFromEdgeInstanceResponse>
      <RequestId>34755DC3-2809-4AE2-BAD8-7B81ED69D570</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</BatchUnbindDeviceFromEdgeInstanceResponse>
```

`JSON` format

```
{
 "RequestId": "34755DC3-2809-4AE2-BAD8-7B81ED69D570",
 "Code": "Success",
 "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

