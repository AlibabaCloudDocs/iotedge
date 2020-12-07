# CreateSceneRule

调用该接口创建场景联动规则。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateSceneRule&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSceneRule|系统规定参数。取值：CreateSceneRule。 |
|RuleName|String|是|test|场景联动规则名称。支持中文、大小写英文字母、数字、下划线（\_）和短划线（-），长度限制为1~30个字符。 |
|RuleDescription|String|否|定时发送消息到钉钉机器人|场景联动规则描述。长度不超过100个字符。 |
|RuleContent|String|否|\{"action":\[\{"params":\{"content":"$\{metadata.formattedTime\}: 收到定时消息","title":"钉钉机器人通知","webHook":"https://oapi.dingtalk.com/robot/send?access\_token=xxxxxxxxx"\},"uri":"action/dingtalk/robot"\}\],"trigger":\{"params":\{"cron":"0 \* \* \* \* ? 2020","cronType":"quartz\_cron"\},"uri":"trigger/timer"\},"type":"IFTTT"\}|场景联动规则内容。格式详情请参见[场景联动规则编写说明](~~171059~~)。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|C9D9C91B-1B3B-4D84-BE58-68E7B2A989EA|阿里云为该请求生成的唯一标识符。 |
|RuleId|String|f041397879ad4d89822811d741\*\*\*\*\*\*|场景联动规则ID。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateSceneRule
&RuleDescription=定时发送消息到钉钉机器人
&RuleContent={"action":[{"params":{"content":"${metadata.formattedTime}: 收到定时消息","title":"钉钉机器人通知","webHook":"https://oapi.dingtalk.com/robot/send?access_token=xxxxxxxxx"},"uri":"action/dingtalk/robot"}],"trigger":{"params":{"cron":"0 * * * * ? 2020","cronType":"quartz_cron"},"uri":"trigger/timer"},"type":"IFTTT"}
&RuleName=test
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateSceneRuleResponse>
    <RequestId>C9D9C91B-1B3B-4D84-BE58-68E7B2A989EA</RequestId>
    <RuleId>f041397879ad4d89822811d741******</RuleId>
    <Code>Success</Code>
    <Success>true</Success>
</CreateSceneRuleResponse>
```

`JSON` 格式

```
{
  "RequestId": "C9D9C91B-1B3B-4D84-BE58-68E7B2A989EA",
  "RuleId": "f041397879ad4d89822811d741******",
  "Code": "Success",
  "Success": true
}
```

