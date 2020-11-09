# UnbindApplicationFromEdgeInstance

调用该接口，从边缘实例中移除边缘应用。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM账号共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UnbindApplicationFromEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UnbindApplicationFromEdgeInstance|系统规定参数。取值：UnbindApplicationFromEdgeInstance。 |
|ApplicationId|String|是|361368ba5a094da9bf5625d092\*\*\*\*\*\*|边缘应用的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**应用管理**页面中，鼠标悬浮在目标应用名称上获取ID。 |
|InstanceId|String|是|Tb4r9k3GWHJFWv\*\*\*\*\*\*|边缘实例的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|5CA3B4EE-D865-47B0-91FD-BA7C2BC6BCC4|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=UnbindApplicationFromEdgeInstance
&InstanceId=Tb4r9k3GWHJFWv******
&ApplicationId=361368ba5a094da9bf5625d092******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UnbindApplicationFromEdgeInstanceResponse>
    <RequestId>5CA3B4EE-D865-47B0-91FD-BA7C2BC6BCC4</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</UnbindApplicationFromEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "5CA3B4EE-D865-47B0-91FD-BA7C2BC6BCC4",
  "Code": "Success",
  "Success": true
}
```

