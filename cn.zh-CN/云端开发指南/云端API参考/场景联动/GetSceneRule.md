# GetSceneRule

调用该接口获取场景联动规则详情。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetSceneRule&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetSceneRule|系统规定参数。取值：GetSceneRule。 |
|RuleId|String|是|f041397879ad4d89822811d741\*\*\*\*\*\*|场景联动规则ID。调用[QuerySceneRule](~~169498~~)接口获取场景联动规则ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时返回的数据。 |
|GmtCreate|Long|1584085921000|场景联动规则的创建时间。 |
|GmtModified|Long|1579493552000|场景联动规则最后一次更新的时间。 |
|RuleContent|String|\{\\"action\\":\[\{\\"params\\":\{\\"productKey\\":\\"a19luLB\*\*\*\*\\",\\"propertyItems\\":\{\\"LightAdjustLevel\\":10\},\\"deviceName\\":\\"test01\\"\},\\"uri\\":\\"action/device/setProperty\\"\}\],\\"trigger\\":\{\\"params\\":\{\\"cron\\":\\"22 13 20 1 \*\\",\\"cronType\\":\\"linux\\"\},\\"uri\\":\\"trigger/timer\\"\},\\"type\\":\\"IFTTT\\",\\"sid\\":\\"9df954b33c854d469a507ef8d6\*\*\*\*\*\*\\"\}|场景联动规则内容。 |
|RuleDescription|String|测试|场景联动规则描述。 |
|RuleName|String|test|场景联动规则的名称。 |
|RuleStatus|Integer|0|场景联动规则在云端的状态。

 -   0：表示停止。
-   1：表示启动。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|1B6D50A7-F160-4D47-863C-EDEE25E26495|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=GetSceneRule
&RuleId=f041397879ad4d89822811d741******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetSceneRuleResponse>
    <RequestId>1B6D50A7-F160-4D47-863C-EDEE25E26495</RequestId>
    <Data>
        <GmtCreate>1584085921000</GmtCreate>
        <GmtModified>1579493552000</GmtModified>
        <RuleContent>{"action":[{"params":{"productKey":"a19luLB****","propertyItems":{"LightAdjustLevel":10},"deviceName":"test01"},"uri":"action/device/setProperty"}],"trigger":{"params":{"cron":"22 13 20 1 *","cronType":"linux"},"uri":"trigger/timer"},"type":"IFTTT","sid":"9df954b33c854d469a507ef8d6******"}</RuleContent>
        <RuleStatus>0</RuleStatus>
        <RuleName>test</RuleName>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</GetSceneRuleResponse>
```

`JSON` 格式

```
{
  "RequestId": "1B6D50A7-F160-4D47-863C-EDEE25E26495",
  "Data": {
    "GmtCreate": 1584085921000,
    "GmtModified": 1579493552000,
    "RuleContent": "{\"action\":[{\"params\":{\"productKey\":\"a19luLB****\",\"propertyItems\":{\"LightAdjustLevel\":10},\"deviceName\":\"test01\"},\"uri\":\"action/device/setProperty\"}],\"trigger\":{\"params\":{\"cron\":\"22 13 20 1 *\",\"cronType\":\"linux\"},\"uri\":\"trigger/timer\"},\"type\":\"IFTTT\",\"sid\":\"9df954b33c854d469a507ef8d6******\"}",
    "RuleStatus": 0,
    "RuleName": "test"
  },
  "Code": "Success",
  "Success": true
}
```

