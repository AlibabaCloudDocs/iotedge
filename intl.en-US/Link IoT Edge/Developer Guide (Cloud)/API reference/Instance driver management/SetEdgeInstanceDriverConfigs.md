# SetEdgeInstanceDriverConfigs

Configures a driver that is bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=SetEdgeInstanceDriverConfigs&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetEdgeInstanceDriverConfigs|The operation that you want to perform. Set the value to SetEdgeInstanceDriverConfigs. |
|Configs.N.Content|String|Yes|\{"test":123\}|The content of the configuration. You can specify one of the following items:

 -   The configuration content. For more information about the format, see [Driver and device configurations](~~120906~~).
-   The Object Storage Service \(OSS\) path of the configuration file. |
|Configs.N.Format|String|Yes|JSON|The format of the configuration. Valid values: KV \(key-value pair\), JSON \(JSON string\), and FILE \(configuration file\). |
|DriverId|String|Yes|021d154d2a2f4dd7a489773d9e04\*\*\*\*|The ID of the driver. To obtain the driver ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of the driver that is bound to the edge instance and obtain the driver ID.

 You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver ID. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that uses the driver and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|Configs.N.Key|String|No|key1|The key of the configuration. If multiple configurations are specified, you can use this parameter to differentiate the configurations. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|252C7754-F6A2-454B-9DE2-382A97FC0C3F|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=SetEdgeInstanceDriverConfigs
&Configs.1.Content={"test":123}
&DriverId=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&Configs.1.Format=JSON
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetEdgeInstanceDriverConfigsResponse>
      <RequestId>252C7754-F6A2-454B-9DE2-382A97FC0C3F</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</SetEdgeInstanceDriverConfigsResponse>
```

`JSON` format

```
{
 "RequestId": "252C7754-F6A2-454B-9DE2-382A97FC0C3F",
 "Code": "Success",
 "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

