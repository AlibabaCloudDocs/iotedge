# QueryEdgeInstanceSceneRule

调用该接口分页查询边缘实例中的场景联动规则列表。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceSceneRule&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceSceneRule|系统规定参数。取值：QueryEdgeInstanceSceneRule。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|InstanceId|String|是|llL44UVXUqb9m5\*\*\*\*\*\*|边缘实例的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|PageSize|Integer|是|10|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|PageSize|Integer|10|返回结果中每页显示的记录数量。 |
|RuleList|Array of Rule| |场景联动规则列表。 |
|GmtCreate|Long|1582004185000|场景联动规则的创建时间。 |
|IsExisted|Integer|1|场景联动规则是否存在。

 -   0：表示已删除。
-   1：表示存在。 |
|RuleId|String|f041397879ad4d89822811d741\*\*\*\*\*\*|场景联动规则ID。 |
|RuleName|String|test|场景联动规则的名称。 |
|Status|Integer|1|场景联动规则在边缘实例中的状态。

 -   0：表示已停止。
-   1：表示已启动。 |
|Total|Integer|1|场景联动规则总数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|D4C3331B-0FA8-4A05-AFE2-54F698EDEAF7|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceSceneRule
&PageSize=10
&InstanceId=llL44UVXUqb9m5******
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryEdgeInstanceSceneRuleResponse>
    <RequestId>D4C3331B-0FA8-4A05-AFE2-54F698EDEAF7</RequestId>
    <Data>
        <RuleList>
            <Rule>
                <GmtCreate>1582004185000</GmtCreate>
                <RuleId>f041397879ad4d89822811d741******</RuleId>
                <GmtModified>1582098176000</GmtModified>
                <RuleStatus>1</RuleStatus>
                <RuleName>test</RuleName>
            </Rule>
        </RuleList>
        <PageSize>10</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>1</Total>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceSceneRuleResponse>
```

`JSON` 格式

```
{
  "RequestId": "D4C3331B-0FA8-4A05-AFE2-54F698EDEAF7",
  "Data": {
    "RuleList": [
      {
        "GmtCreate": "1582004185000",
        "RuleId": "f041397879ad4d89822811d741******",
        "GmtModified": "1582098176000",
        "RuleStatus": 1,
        "RuleName": "test"
      }
    ],
    "PageSize": 10,
    "CurrentPage": 1,
    "Total": 1
  },
  "Code": "Success",
  "Success": true
}
```

