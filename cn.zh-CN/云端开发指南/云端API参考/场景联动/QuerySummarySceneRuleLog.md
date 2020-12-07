# QuerySummarySceneRuleLog

调用该接口查询场景联动规则日志。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QuerySummarySceneRuleLog&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QuerySummarySceneRuleLog|系统规定参数。取值：QuerySummarySceneRuleLog。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|RuleId|String|是|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|场景联动规则ID。调用[QuerySceneRule](~~169498~~)接口获取场景联动规则ID。 |
|StartTime|Integer|是|1582372973|场景联动规则日志的开始时间，单位为秒，输入Unix时间戳。

 **说明：** 最多可查询近一个月（30天）的规则执行日志。 |
|EndTime|Integer|是|1582373873|场景联动规则日志的结束时间，单位为秒，输入Unix时间戳。

 **说明：** 最多可查询近一个月（30天）的规则执行日志。 |
|PageSize|Integer|是|10|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|Status|String|是|2|场景联动规则的执行结果。

 -   0：表示失败。
-   1：表示成功。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|2279A994-3E7D-4EC6-BD17-FA0D0EC2EC77|阿里云为该请求生成的唯一标识符。 |
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|LogList|Array of LogInfo| |场景联动规则日志列表。 |
|LogInfo| | | |
|LogTime|Integer|1582373706|场景联动规则日志出现的时间。 |
|Result|String|true|场景联动规则的执行结果。

 -   true：表示成功。
-   false：表示失败。 |
|TraceId|String|a6a5b5df1582373508176121\*\*\*\*\*\*|场景联动规则日志的轨迹ID。 |
|PageSize|Integer|10|返回结果中每页显示的记录数量。 |
|Total|Integer|3|场景联动规则日志总数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QuerySummarySceneRuleLog
&EndTime=1582373873
&PageSize=10
&CurrentPage=1
&RuleId=fec565038d7544978d9aed5c1a******
&StartTime=1582372973
&status=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QuerySummarySceneRuleLogResponse>
    <RequestId>2279A994-3E7D-4EC6-BD17-FA0D0EC2EC77</RequestId>
    <Data>
        <LogList>
            <LogInfo>
                <LogTime>1582373706</LogTime>
                <TraceId>a6a5b5df1582373508176121******</TraceId>
                <Result>true</Result>
            </LogInfo>
            <LogInfo>
                <LogTime>1582373411</LogTime>
                <TraceId>90c8f97a1582373433359109******</TraceId>
                <Result>true</Result>
            </LogInfo>
            <LogInfo>
                <LogTime>1582373408</LogTime>
                <TraceId>90c8f97a1582373411302109******</TraceId>
                <Result>true</Result>
            </LogInfo>
        </LogList>
        <PageSize>10</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>3</Total>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QuerySummarySceneRuleLogResponse>
```

`JSON` 格式

```
{
  "RequestId": "2279A994-3E7D-4EC6-BD17-FA0D0EC2EC77",
  "Data": {
    "LogList": [
      {
        "LogTime": 1582373706,
        "TraceId": "a6a5b5df1582373508176121******",
        "Result": "true"
      },
      {
        "LogTime": 1582373411,
        "TraceId": "90c8f97a1582373433359109******",
        "Result": "true"
      },
      {
        "LogTime": 1582373408,
        "TraceId": "90c8f97a1582373411302109******",
        "Result": "true"
      }
    ],
    "PageSize": 10,
    "CurrentPage": 1,
    "Total": 3
  },
  "Code": "Success",
  "Success": true
}
```

