# QueryEdgeInstanceDevice

查询边缘实例中的设备列表。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceDevice|系统规定参数。取值：QueryEdgeInstanceDevice。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值是1。 |
|InstanceId|String|是|tG7sKuOQ7ylb7qS4\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|PageSize|Integer|是|15|返回结果中，每页显示的记录数量。最大取值30，最小取值1，默认取值为10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|DeviceList|Array of Device| |设备信息列表。 |
|DeviceName|String|test\_tmp\_zdy|设备名称。 |
|DriverId|String|44c090ba7b104641a4b9bcf10241\*\*\*\*|驱动ID。 |
|IotId|String|XSpPdtxzE6ebtCkx\*\*\*\*000101|设备ID。 |
|ProductKey|String|a1p5QfE\*\*\*\*|产品的唯一标识符。 |
|PageSize|Integer|15|返回结果中每页显示的设备数量。 |
|Total|Integer|4|设备数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|AC76932E-E0C9-41EE-843D-B1CA3279B053|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceDevice
&PageSize=15
&InstanceId=tG7sKuOQ7ylb7qS4****
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

