# BatchGetEdgeInstanceDriverConfigs

Queries the configuration information of one or more drivers that are bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BatchGetEdgeInstanceDriverConfigs&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchGetEdgeInstanceDriverConfigs|The operation that you want to perform. Set the value to BatchGetEdgeInstanceDriverConfigs. |
|DriverIds.N|RepeatList|Yes|021d154d2a2f4dd7a489773d9e04\*\*\*\*|The IDs of the drivers that you want to query. To obtain the driver IDs, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of each driver whose configurations you want to query and obtain the driver ID.

 You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver IDs.

 **Note:** You can specify a maximum of 20 driver IDs. This means that you can obtain the configuration information of a maximum of 20 drivers at a time. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that uses the drivers and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|DriverConfigList|Array of DriverConfig| |The data that is returned if the call was successful. |
|ConfigList|Array of Config| |The configuration information of the driver. |
|ConfigId|String|dac71722ceac4a299dbf3e8dc3c8\*\*\*\*|The ID of the configuration. |
|Content|String|\{\\"test\\":123\}|The configuration content or the Object Storage Service \(OSS\) path of the configuration file. |
|Format|String|JSON|The format of the configuration. Valid values: KV \(key-value pair\), JSON \(JSON string\), and FILE \(configuration file\). |
|Key|String|key1|The key of the configuration. If multiple configurations are available, keywords can be used to identify the configurations. |
|DriverId|String|021d154d2a2f4dd7a489773d9e04\*\*\*\*|The ID of the driver. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|D6113390-F507-458B-8544-7B01F945630B|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=BatchGetEdgeInstanceDriverConfigs
&DriverIds.1=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchGetEdgeInstanceDriverConfigsResponse>
    <DriverConfigList>
        <DriverConfig>
            <DriverId>021d154d2a2f4dd7a489773d9e0****c</DriverId>
            <ConfigList>
                <Config>
                    <Format>JSON</Format>
                    <Content>{"test":123}</Content>
                    <ConfigId>dac71722ceac4a299dbf3e8dc3c8****</ConfigId>
                </Config>
            </ConfigList>
        </DriverConfig>
    </DriverConfigList>
    <RequestId>D6113390-F507-458B-8544-7B01F945630B</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</BatchGetEdgeInstanceDriverConfigsResponse>
```

`JSON` format

```
{
  "DriverConfigList": [
    {
      "DriverId": "021d154d2a2f4dd7a489773d9e04****",
      "ConfigList": [
        {
          "Format": "JSON",
          "Content": "{\"test\":123}",
          "ConfigId": "dac71722ceac4a299dbf3e8dc3c8****"
        }
      ]
    }
  ],
  "RequestId": "D6113390-F507-458B-8544-7B01F945630B",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

