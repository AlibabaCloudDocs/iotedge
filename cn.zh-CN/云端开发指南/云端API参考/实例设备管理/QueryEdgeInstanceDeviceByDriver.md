# QueryEdgeInstanceDeviceByDriver

调用该接口查询驱动下关联的子设备。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceDeviceByDriver&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceDeviceByDriver|系统规定参数。取值：QueryEdgeInstanceDeviceByDriver。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|DriverId|String|是|9c1ae7bd59f1469abbdccc9592\*\*\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|6GaTtvTj7vJhiS\*\*\*\*\*\*|边缘实例的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|PageSize|Integer|是|15|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |
|ChannelId|String|否|BE0BD49EF5EF4D119D09CC1B25\*\*\*\*\*\*|驱动通道ID。调用[QueryEdgeInstanceChannel](~~162253~~)接口获取。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|DeviceList|Array of Device| |子设备信息列表。 |
|IotId|String|Hathoyxglj9jpYPyw3WN\*\*\*\*\*\*|子设备ID。 |
|PageSize|Integer|15|返回结果中每页显示的记录数量。 |
|Total|Integer|1|驱动下关联的子设备总数。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|C2AEE142-A9ED-46C5-9EA4-BF0817F0D556|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceDeviceByDriver
&DriverId=9c1ae7bd59f1469abbdccc9592******
&PageSize=15
&InstanceId=6GaTtvTj7vJhiS******
&CurrentPage=1
&ChannelId=BE0BD49EF5EF4D119D09CC1B25******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryEdgeInstanceDeviceByDriverResponse>
    <RequestId>C2AEE142-A9ED-46C5-9EA4-BF0817F0D556</RequestId>
    <Data>
        <PageSize>15</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>1</Total>
        <DeviceList>
            <Device>
                <IotId>Hathoyxglj9jpYPyw3WN******</IotId>
            </Device>
        </DeviceList>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceDeviceByDriverResponse>
```

`JSON` 格式

```
{
  "RequestId": "C2AEE142-A9ED-46C5-9EA4-BF0817F0D556",
  "Data": {
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 1,
    "DeviceList": [
      {
        "IotId": "Hathoyxglj9jpYPyw3WN******"
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

