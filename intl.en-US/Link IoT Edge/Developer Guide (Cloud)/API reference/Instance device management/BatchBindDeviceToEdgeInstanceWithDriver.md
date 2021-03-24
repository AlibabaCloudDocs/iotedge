# BatchBindDeviceToEdgeInstanceWithDriver

Binds multiple devices to an edge instance and configures a driver for the devices.

## Limits

Each Alibaba Cloud account can run a maximum of five queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=BatchBindDeviceToEdgeInstanceWithDriver&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchBindDeviceToEdgeInstanceWithDriver|The operation that you want to perform. Set the value to BatchBindDeviceToEdgeInstanceWithDriver. |
|DriverId|String|Yes|021d154d2a2f4dd7a489773d9e04\*\*\*\*|The ID of the driver. To obtain the driver ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of the driver that you want to configure and obtain the driver ID.

You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver ID. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance to which you want to bind multiple devices and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotIds.N|RepeatList|Yes|BXPV9Ks3bxwM9fD\*\*\*\*0000101|The IDs of the devices.

You can call the [QueryDevice](~~69905~~) operation to query detailed information about all devices that belong to the current Alibaba Cloud account and obtain the required device IDs.

**Note:** You can specify a maximum of 20 device IDs when you call the BatchBindDeviceToEdgeInstanceWithDriver operation. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|BFFA9519-6AF1-4D15-AFAF-FD412714C1BE|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=BatchBindDeviceToEdgeInstanceWithDriver
&IotIds.3=BXPV9Ks3bxwM9fD****0000101
&IotIds.2=sjI0Sd124XFYyjB****O000101
&IotIds.1=8n5sFqlfnchlBjct****000101
&DriverId=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchBindDeviceToEdgeInstanceWithDriverResponse>
      <RequestId>BFFA9519-6AF1-4D15-AFAF-FD412714C1BE</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</BatchBindDeviceToEdgeInstanceWithDriverResponse>
```

`JSON` format

```
{
 "RequestId": "BFFA9519-6AF1-4D15-AFAF-FD412714C1BE",
 "Code": "Success",
 "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

