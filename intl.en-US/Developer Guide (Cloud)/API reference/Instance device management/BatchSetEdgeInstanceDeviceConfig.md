# BatchSetEdgeInstanceDeviceConfig

Configures multiple devices of an edge instance.

## Limits

A single Alibaba Cloud account can run a maximum of 5 queries per second \(QPS\).

**Note:** RAM users share the quota of the Alibaba Cloud account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BatchSetEdgeInstanceDeviceConfig&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchSetEdgeInstanceDeviceConfig|The operation that you want to perform. Set the value to BatchSetEdgeInstanceDeviceConfig. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for public instances. However, this parameter is required for the instances that you have purchased. |
|DeviceConfigs.N.IotId|String|No|sjI0Sd124XFYyjBY\*\*\*\*000101|The ID of the device.

You can call the [QueryEdgeInstanceDevice]() operation to query edge instance devices. |
|DeviceConfigs.N.Content|String|No|\{"test": "device\_config\_demo"\}|The information of the configuration. You can specify either of the following values:

-   The configuration content.
-   The Object Storage Service \(OSS\) path of the configuration file. |

In addition to the preceding exclusive request parameters, you must specify common request parameters when calling this API operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|748659E2-EDC9-4E3E-BF9D-06F16995CF66|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. true: indicates that the call was successful. false: indicates that the call failed. |
|Code|String|Success|The error code. Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message returned if the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=BatchSetEdgeInstanceDeviceConfig
&InstanceId=F3APY0tPLhmgGtx0****
&DeviceConfigs.1.IotId=sjI0Sd124XFYyjBY****000101
&DeviceConfigs.2.IotId=BXPV9Ks3bxwM9fD****0000101
&DeviceConfigs.1.Content={"test": "device_config_demo"}
&DeviceConfigs.2.Content={"test": "device_config_demo"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchSetEdgeInstanceDeviceConfigResponse>
      <RequestId>748659E2-EDC9-4E3E-BF9D-06F16995CF66</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</BatchSetEdgeInstanceDeviceConfigResponse>
```

`JSON` format

```
{
 "RequestId": "748659E2-EDC9-4E3E-BF9D-06F16995CF66",
 "Code": "Success",
 "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

