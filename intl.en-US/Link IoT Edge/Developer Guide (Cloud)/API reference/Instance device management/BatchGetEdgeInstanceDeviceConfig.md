# BatchGetEdgeInstanceDeviceConfig

Queries the configuration information of one or more devices that are bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of five queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BatchGetEdgeInstanceDeviceConfig&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchGetEdgeInstanceDeviceConfig|The operation that you want to perform. Set the value to BatchGetEdgeInstanceDeviceConfig. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that you want to query and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotIds.N|RepeatList|Yes|BXPV9Ks3bxwM9fDl\*\*\*\*000101|The IDs of the devices. You can call the [QueryEdgeInstanceDevice](~~135261~~) operation to query the IDs of the devices that are bound to an edge instance.

**Note:** You can specify a maximum of 20 device IDs when you call the BatchGetEdgeInstanceDeviceConfig operation. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|DeviceConfigList|Array of DeviceConfig| |The device configuration information that is returned if the call was successful. |
|Config|Struct| |The configuration information of the device. |
|Content|String|\{\\"test\\": \\"device\_config\_demo\\"\}|The configuration content or the Object Storage Service \(OSS\) path of the configuration file. |
|Format|String|JSON|The format of the configuration. Valid values: KV \(key-value pair\), JSON \(JSON string\), and FILE \(configuration file\). |
|IotId|String|sjI0Sd124XFYyjBY\*\*\*\*000101|The ID of the device. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|D4A102C2-36A5-4964-9694-0F8EFF95CCA8|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=BatchGetEdgeInstanceDeviceConfig
&IotIds.2=BXPV9Ks3bxwM9fDl****000101
&IotIds.1=sjI0Sd124XFYyjBY****000101
&InstanceId=F3APY0tPLhmgGtx0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchGetEdgeInstanceDeviceConfigResponse>
    <DeviceConfigList>
        <DeviceConfig>
            <IotId>sjI0Sd124XFYyjBY****000101</IotId>
            <Config>
                <Format>JSON</Format>
                <Content>{"test": "device_config_demo"}</Content>
            </Config>
        </DeviceConfig>
        <DeviceConfig>
            <IotId>BXPV9Ks3bxwM9fD****0000101</IotId>
            <Config>
                <Format>JSON</Format>
                <Content>{"test": "device_config_demo"}</Content>
            </Config>
        </DeviceConfig>
    </DeviceConfigList>
    <RequestId>D4A102C2-36A5-4964-9694-0F8EFF95CCA8</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</BatchGetEdgeInstanceDeviceConfigResponse>
```

`JSON` format

```
{
  "DeviceConfigList": [
    {
      "IotId": "sjI0Sd124XFYyjBY****000101",
      "Config": {
        "Format": "JSON",
        "Content": "{\"test\": \"device_config_demo\"}"
      }
    },
    {
      "IotId": "BXPV9Ks3bxwM9fD****0000101",
      "Config": {
        "Format": "JSON",
        "Content": "{\"test\": \"device_config_demo\"}"
      }
    }
  ],
  "RequestId": "D4A102C2-36A5-4964-9694-0F8EFF95CCA8",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

