# BindGatewayToEdgeInstance

Binds a gateway to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BindGatewayToEdgeInstance&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BindGatewayToEdgeInstance|The operation that you want to perform. Set the value to BindGatewayToEdgeInstance. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance to which you want to bind a gateway and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|ProductKey|String|No|a1mAdeG\*\*\*\*|The key that uniquely identifies the product to which the gateway belongs.

**Note:** If you specify this parameter, you must also specify the **DeviceName** parameter. |
|DeviceName|String|No|device1|The name of the gateway.

**Note:** If you specify this parameter, you must also specify the **ProductKey** parameter. |
|IotId|String|No|4z819VQHk6VSLmmBJfrf0010\*\*\*\*\*\*|The ID of the gateway in IoT Platform. This parameter corresponds to the combination of the **ProductKey** and **DeviceName** parameters.

**Note:** If you specify this parameter, you do not need to specify the **ProductKey** or **DeviceName** parameter. If you use the **IotId** parameter and the combination of the **ProductKey** and **DeviceName** parameters, only the **IotId** parameter takes effect. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|28D159F4-980F-423D-95F0-F705E9DFC016|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=BindGatewayToEdgeInstance
&InstanceId=F3APY0tPLhmgGtx0****
&ProductKey=a1mAdeG****
&DeviceName=e46ea1a4347c42a0a83b8c956ab1ab
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BindGatewayToEdgeInstanceResponse>
      <RequestId>E3817065-2A17-4814-82FA-66FAB2CC01DF</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</BindGatewayToEdgeInstanceResponse>
```

`JSON` format

```
{
  "RequestId": "E3817065-2A17-4814-82FA-66FAB2CC01DF",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

