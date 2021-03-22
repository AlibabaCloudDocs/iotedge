# QueryEdgeInstanceGateway

Queries the gateways that are bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceGateway&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryEdgeInstanceGateway|The operation that you want to perform. Set the value to QueryEdgeInstanceGateway. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that you want to query and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|GatewayList|Array of Gateway| |The data that is returned if the call was successful. |
|DeviceName|String|gateway\_01|The name of the gateway. |
|EdgeVersion|String|v1.0.0|The version number of Link IoT Edge. |
|IotId|String|LuD9x5hiRUdVemWU\*\*\*\*000101|The ID of the gateway in IoT Platform. |
|ProductKey|String|a1mAdeG\*\*\*\*|The key that uniquely identifies the product to which the gateway belongs. |
|RequestId|String|28D159F4-980F-423D-95F0-F705E9DFC016|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=QueryEdgeInstanceGateway
&InstanceId=F3APY0tPLhmgGtx0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryEdgeInstanceGatewayResponse>
    <GatewayList>
        <Gateway>
            <IotId>LuD9x5hiRUdVemWU****000101</IotId>
            <ProductKey>a1mAdeG****</ProductKey>
            <DeviceName>gateway_01</DeviceName>
            <EdgeVersion>v1.0.0</EdgeVersion>
        </Gateway>
    </GatewayList>
    <RequestId>547A62E5-0D6D-4DB5-9CCC-58C706891976</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceGatewayResponse>
```

`JSON` format

```
{
  "GatewayList": [
    {
      "IotId": "LuD9x5hiRUdVemWU****000101",
      "ProductKey": "a1mAdeG****",
      "DeviceName": "gateway_01",
      "EdgeVersion": "v1.0.0"
    }
  ],
  "RequestId": "547A62E5-0D6D-4DB5-9CCC-58C706891976",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

