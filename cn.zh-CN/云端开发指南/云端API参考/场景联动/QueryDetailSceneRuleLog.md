# QueryDetailSceneRuleLog

调用该接口查看场景联动规则日志的详细信息。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDetailSceneRuleLog&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDetailSceneRuleLog|系统规定参数。取值：QueryDetailSceneRuleLog。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|StartTime|Integer|是|1581917582|场景联动规则日志的开始时间，单位为秒，输入Unix时间戳。

 **说明：** 最多可查询近一个月（30天）的规则执行日志。 |
|EndTime|Integer|是|1581918482|场景联动规则日志的结束时间，单位为秒，输入Unix时间戳。

 **说明：** 最多可查询近一个月（30天）的规则执行日志。 |
|RuleId|String|是|e5dd1c7aa3994ecdbc88235979\*\*\*\*\*\*|场景联动规则ID。调用[QuerySceneRule](~~169498~~)接口获取场景联动规则ID。 |
|PageSize|Integer|是|15|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|TraceId|String|是|b662a9671581918480168107\*\*\*\*\*\*|场景联动规则日志的轨迹ID。调用[QuerySummarySceneRuleLog](~~169511~~)接口获取该ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|LogList|Array of LogInfo| |场景联动规则日志详情列表。 |
|Code|String|9201|接口返回码。200表示成功，其它表示错误码，详情请参见**Message**参数中的错误信息提示。 |
|Message|String|device offline, productKey: a1c3t\*\*\*\*, deviceName: my\_device1|接口返回的场景联动规则日志信息。 |
|PkDn|String|a1c3t\*\*\*\*/my\_device1|场景联动关联的子设备ProductKey和DeviceName。格式为`your_ProductKey/your_DeviceName`。 |
|PageSize|Integer|15|返回结果中每页显示的记录数量。 |
|Total|Integer|1|场景联动规则日志总数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|ED2DF141-B09A-4C8A-BAA5-30CCEE63036C|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryDetailSceneRuleLog
&EndTime=1581918482
&PageSize=15
&regionId=cn-shanghai
&CurrentPage=1
&RuleId=e5dd1c7aa3994ecdbc88235979******
&StartTime=1581917582
&TraceId=b662a9671581918480168107******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDetailSceneRuleLogResponse>
    <RequestId>ED2DF141-B09A-4C8A-BAA5-30CCEE63036C</RequestId>
    <Data>
        <LogList>
            <LogInfo>
                <PkDn>a1c3t****/my_device1</PkDn>
                <Message>device offline, productKey: a1c3****, deviceName: my_device1</Message>
                <Code>9201</Code>
            </LogInfo>
        </LogList>
        <PageSize>15</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>1</Total>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryDetailSceneRuleLogResponse>
```

`JSON` 格式

```
{
  "RequestId": "ED2DF141-B09A-4C8A-BAA5-30CCEE63036C",
  "Data": {
    "LogList": [
      {
        "PkDn": "a1c3t****/my_device1",
        "Message": "device offline, productKey: a1c3t****, deviceName: my_device1",
        "Code": "9201"
      }
    ],
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 1
  },
  "Code": "Success",
  "Success": true
}
```

