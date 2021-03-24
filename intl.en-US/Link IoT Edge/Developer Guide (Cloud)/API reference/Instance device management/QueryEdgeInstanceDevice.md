# QueryEdgeInstanceDevice

Queries the devices that are bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceDevice&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryEdgeInstanceDevice|The operation that you want to perform. Set the value to QueryEdgeInstanceDevice. |
|CurrentPage|Integer|Yes|1|The number of the page to return. Pages start from Page 1. |
|InstanceId|String|Yes|tG7sKuOQ7ylb7qS4\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that you want to query and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|PageSize|Integer|Yes|15|The number of entries to return on each page. Valid values: 1 to 30. Default value: 10. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|CurrentPage|Integer|1|The page number of the returned page. |
|DeviceList|Array of Device| |The list of device information. |
|DeviceName|String|test\_tmp\_zdy|The name of the device. |
|DriverId|String|44c090ba7b104641a4b9bcf10241\*\*\*\*|The ID of the driver. |
|IotId|String|XSpPdtxzE6ebtCkx\*\*\*\*000101|The ID of the device. |
|ProductKey|String|a1p5QfE\*\*\*\*|The key that uniquely identifies the product to which the device belongs. |
|PageSize|Integer|15|The number of entries returned per page. |
|Total|Integer|4|The number of devices. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|AC76932E-E0C9-41EE-843D-B1CA3279B053|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=QueryEdgeInstanceDevice
&PageSize=15
&InstanceId=tG7sKuOQ7ylb7qS4****
&CurrentPage=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryEdgeInstanceDeviceResponse>
    <RequestId>AC76932E-E0C9-41EE-843D-B1CA3279B053</RequestId>
    <Data>
        <PageSize>15</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>4</Total>
        <DeviceList>
            <Device>
                <IotId>XSpPdtxzE6ebtCkx****000101</IotId>
                <DriverId>44c090ba7b104641a4b9bcf10241****</DriverId>
                <ProductKey>a1p5QfE****</ProductKey>
                <DeviceName>test_tmp_zdy</DeviceName>
            </Device>
            <Device>
                <IotId>ixX7TRWtewDxZnus****000101</IotId>
                <DriverId>021d154d2a2f4dd7a489773d9e04****</DriverId>
                <ProductKey>a1p5QfE****</ProductKey>
                <DeviceName>test_name19</DeviceName>
            </Device>
            <Device>
                <IotId>MkzMNGVF3wOk62J6****000101</IotId>
                <DriverId>021d154d2a2f4dd7a489773d9e04****</DriverId>
                <ProductKey>a11jTlJ****</ProductKey>
                <DeviceName>testsss</DeviceName>
            </Device>
            <Device>
                <IotId>6nFJ9ewglx7aBWPb****000101</IotId>
                <DriverId>021d154d2a2f4dd7a489773d9e04****</DriverId>
                <ProductKey>a1PcD3R****</ProductKey>
                <DeviceName>device01</DeviceName>
            </Device>
        </DeviceList>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceDeviceResponse>
```

`JSON` format

```
{
  "RequestId": "AC76932E-E0C9-41EE-843D-B1CA3279B053",
  "Data": {
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 4,
    "DeviceList": [
      {
        "IotId": "XSpPdtxzE6ebtCkx****000101",
        "DriverId": "44c090ba7b104641a4b9bcf10241****",
        "ProductKey": "a1p5QfE****",
        "DeviceName": "test_tmp_zdy"
      },
      {
        "IotId": "ixX7TRWtewDxZnus****000101",
        "DriverId": "021d154d2a2f4dd7a489773d9e04****",
        "ProductKey": "a1p5QfE****",
        "DeviceName": "test_name19"
      },
      {
        "IotId": "MkzMNGVF3wOk62J6****000101",
        "DriverId": "021d154d2a2f4dd7a489773d9e04****",
        "ProductKey": "a11jTlJ****",
        "DeviceName": "testsss"
      },
      {
        "IotId": "6nFJ9ewglx7aBWPb****000101",
        "DriverId": "021d154d2a2f4dd7a489773d9e04****",
        "ProductKey": "a1PcD3R****",
        "DeviceName": "device01"
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

