# BatchSetEdgeInstanceDeviceConfig

Configures multiple devices that are bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of five queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BatchSetEdgeInstanceDeviceConfig&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchSetEdgeInstanceDeviceConfig|The operation that you want to perform. Set the value to BatchSetEdgeInstanceDeviceConfig. |
|DeviceConfigs.N.Content|String|Yes|\{"test": "device\_config\_demo"\}|The content of the configuration. You can specify one of the following items:

 -   The configuration content. For more information about the format, see [Device configurations](~~172319~~).
-   The Object Storage Service \(OSS\) path of the configuration file.

 **Note:** You can specify a maximum of 20 device configurations when you call this operation. |
|DeviceConfigs.N.IotId|String|Yes|sjI0Sd124XFYyjBY\*\*\*\*000101|The IDs of the devices.

 You can call the [QueryEdgeInstanceDevice](~~135261~~) operation to query the IDs of the devices that are bound to an edge instance.

 **Note:** You can specify a maximum of 20 device IDs when you call this operation. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance for which you want to configure multiple devices and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|748659E2-EDC9-4E3E-BF9D-06F16995CF66|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

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

