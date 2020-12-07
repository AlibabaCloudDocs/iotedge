# BatchSetEdgeInstanceDeviceChannel

调用该接口批量关联驱动通道到子设备。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchSetEdgeInstanceDeviceChannel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchSetEdgeInstanceDeviceChannel|系统规定参数。取值：BatchSetEdgeInstanceDeviceChannel。 |
|ChannelId|String|是|BE0BD49EF5EF4D119D09CC1B25\*\*\*\*\*\*|驱动通道ID。调用[QueryEdgeInstanceChannel](~~162253~~)接口获取。 |
|DriverId|String|是|9c1ae7bd59f1469abbdccc9592\*\*\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|6GaTtvTj7vJhiS\*\*\*\*\*\*|边缘实例的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotIds.N|RepeatList|是|Hathoyxglj9jpYPyw3WN\*\*\*\*\*\*|子设备ID列表。可调用[QueryDevice](~~69905~~)接口查询子设备ID。

 **说明：** 单次调用最多可填写20个子设备ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|B0325EA9-671C-460B-B0F3-83F41CFF855B|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchSetEdgeInstanceDeviceChannel
&DriverId=9c1ae7bd59f1469abbdccc9592******
&IotIds.1=Hathoyxglj9jpYPyw3WN******
&InstanceId=6GaTtvTj7vJhiS3ZDBF4
&ChannelId=BE0BD49EF5EF4D119D09CC1B25******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchSetEdgeInstanceDeviceChannelResponse>
    <RequestId>B0325EA9-671C-460B-B0F3-83F41CFF855B</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</BatchSetEdgeInstanceDeviceChannelResponse>
```

`JSON` 格式

```
{
  "RequestId": "B0325EA9-671C-460B-B0F3-83F41CFF855B",
  "Code": "Success",
  "Success": true
}
```

