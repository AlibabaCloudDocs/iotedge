# UpdateEdgeInstance

调用该接口更新边缘实例。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateEdgeInstance|系统规定参数。取值：UpdateEdgeInstance。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|Name|String|是|LinkIoTEdge\_Node|边缘实例名称。

 支持中文汉字、英文大小写、数字、下划线（\_）和短划线（-），不超过20个字符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Tags|String|否|k1:v1,k2:v2|边缘实例标签。每个标签由`key:value`组成，多个标签间以英文逗号隔开。例如`k1:v1,k2:v2`。

 -   标签key限制如下：
    -   不可为空。
    -   在该边缘实例中唯一。
    -   仅支持英文大小写。
    -   不可超过20个字符。
-   标签value限制如下：
    -   不可为空。
    -   支持中文、英文大小写、数字、下划线（\_）和短划线（-）。
    -   不可超过20个字符（一个中文汉字算2个字符）。

 为空时表示不更新该参数。 |
|Spec|Integer|否|10|产品规格。

 -   10：轻量版。
-   20：标准版。
-   30：专业版。

 为空时表示不更新该参数。 |
|BizEnable|Boolean|否|true|是否开启边缘实例。可选值：

 -   true：开启。
-   false：关闭。

 为空时表示不更新该参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|10CA6DAD-EBAF-4D3E-9309-9DB5B0FF48F2|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=UpdateEdgeInstance
&InstanceId=F3APY0tPLhmgGtx0****
&Spec=30
&Tags=room:1,floor:1
&BizEnable=true
&Name=测试实例new
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateEdgeInstanceResponse>
      <RequestId>10CA6DAD-EBAF-4D3E-9309-9DB5B0FF48F2</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</UpdateEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "10CA6DAD-EBAF-4D3E-9309-9DB5B0FF48F2",
  "Code": "Success",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

