# TriggerSceneRule

调用该接口触发场景联动规则。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=TriggerSceneRule&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|TriggerSceneRule|系统规定参数。取值：TriggerSceneRule。 |
|RuleId|String|是|f041397879ad4d89822811d741\*\*\*\*\*\*|场景联动规则ID。调用[QuerySceneRule](~~169498~~)接口获取场景联动规则ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|InstanceId|String|否|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在物联网平台控制台的**边缘计算** \> **边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|C9D9C91B-1B3B-4D84-AE58-68E7BAA989EK|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=TriggerSceneRule
&RuleId=f041397879ad4d89822811d741******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<TriggerSceneRuleResponse>
    <RequestId>C9D9C91B-1B3B-4D84-AE58-68E7BAA989EK</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</TriggerSceneRuleResponse>
```

`JSON` 格式

```
{
  "RequestId": "C9D9C91B-1B3B-4D84-AE58-68E7BAA989EK",
  "Code": "Success",
  "Success": true
}
```

