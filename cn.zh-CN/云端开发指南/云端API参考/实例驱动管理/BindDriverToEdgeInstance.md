# BindDriverToEdgeInstance

调用该接口将驱动分配到边缘实例中。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BindDriverToEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BindDriverToEdgeInstance|系统规定参数。取值：BindDriverToEdgeInstance。 |
|DriverId|String|是|9c1ae7bd59f1469abbdccc959228\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DriverVersion|String|否|2.0.0|驱动版本号。为空则默认为最新版本驱动。 |
|OrderId|String|否|11123458765\*\*\*\*|订单编号。

 **说明：** 当驱动为已购驱动时必填；驱动为官方驱动或自研驱动时不需要填写。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|28D159F4-980F-423D-95F0-F705E9DFC016|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BindDriverToEdgeInstance
&DriverId=9c1ae7bd59f1469abbdccc959228****
&InstanceId=F3APY0tPLhmgGtx0****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BindDriverToEdgeInstanceResponse>
      <RequestId>FEA6A369-2E16-4DB3-A0A6-6D14FD244170</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</BindDriverToEdgeInstanceResponse>
```

`JSON` 格式

```
{
 "RequestId": "FEA6A369-2E16-4DB3-A0A6-6D14FD244170",
 "Code": "Success",
 "Success": true
}
```

