# DeleteEdgeDriverVersion

Deletes a driver version.

## Limits

-   You are not allowed to delete a published driver version.
-   Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=DeleteEdgeDriverVersion&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteEdgeDriverVersion|The operation that you want to perform. Set the value to DeleteEdgeDriverVersion. |
|DriverId|String|Yes|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|The ID of the driver. To obtain the driver ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of the driver for which you want to delete a driver version and obtain the driver ID.

 You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver ID. |
|DriverVersion|String|Yes|1.2.0|The version number of the driver. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~135196~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|J82E857F-T6B9-4FDE-96B8-E4BE97095D1A|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=DeleteEdgeDriverVersion
&DriverId=fec565038d7544978d9aed5c1a******
&DriverVersion=1.2.0
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteEdgeDriverVersionResponse>
      <RequestId>J82E857F-T6B9-4FDE-96B8-E4BE97095D1A</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</DeleteEdgeDriverVersionResponse>
```

`JSON` format

```
{
  "RequestId": "J82E857F-T6B9-4FDE-96B8-E4BE97095D1A",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

