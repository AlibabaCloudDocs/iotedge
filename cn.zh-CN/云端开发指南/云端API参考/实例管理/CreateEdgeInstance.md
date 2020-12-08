# CreateEdgeInstance

调用该接口创建边缘实例。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateEdgeInstance|系统规定参数。取值：CreateEdgeInstance。 |
|Name|String|是|LinkIoTEdge\_Node|边缘实例名称。

 支持中文汉字、英文大小写、数字、下划线（\_）和短划线（-），不超过20个字符（一个中文汉字算2个字符）。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Tags|String|否|k1:v1,k2:v2|边缘实例标签。每个标签由`key:value`组成，多个标签间以英文逗号隔开。如`k1:v1,k2:v2`。

 -   标签key限制如下：
    -   不可为空。
    -   在该边缘实例中唯一。
    -   仅支持英文大小写。
    -   不可超过20个字符。
-   标签value限制如下：
    -   不可为空。
    -   支持中文、英文大小写、数字、下划线（\_）和短划线（-）。
    -   不可超过20个字符（一个中文汉字算2个字符）。 |
|Spec|Integer|否|20|产品规格。

 -   10：轻量版。
-   20：标准版。
-   30：专业版。

 默认值为20（标准版）。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|InstanceId|String|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。 |
|RequestId|String|28D159F4-980F-423D-95F0-F705E9DFC016|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeInstance
&Spec=30
&Tags=k1:v1,k2:v2
&Name=测试实例
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateEdgeInstanceResponse>
      <RequestId>28D159F4-980F-423D-95F0-F705E9DFC016</RequestId>
      <InstanceId>F3APY0tPLhmgGtx0****</InstanceId>
      <Code>Success</Code>
      <Success>true</Success>
</CreateEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "28D159F4-980F-423D-95F0-F705E9DFC016",
  "InstanceId": "F3APY0tPLhmgGtx0****",
  "Code": "Success",
  "Success": true
}
```

