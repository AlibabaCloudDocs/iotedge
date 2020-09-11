# DeleteEdgeDriver

调用该接口删除已创建的驱动。

## 限制条件

-   当驱动下存在已发布的驱动版本时，该驱动无法删除。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** 子账号共享主账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteEdgeDriver&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteEdgeDriver|系统规定参数。取值：DeleteEdgeDriver。 |
|DriverId|String|是|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。在物联网平台控制台的**边缘计算** \> **驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|F82E857F-B6B9-4CCC-96B8-E4BE97095F1A|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=DeleteEdgeDriver
&DriverId=fec565038d7544978d9aed5c1a******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteEdgeDriverResponse>
      <RequestId>F82E857F-B6B9-4CCC-96B8-E4BE97095F1A</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</DeleteEdgeDriverResponse>
```

`JSON` 格式

```
{
  "RequestId": "F82E857F-B6B9-4CCC-96B8-E4BE97095F1A",
  "Code": "Success",
  "Success": true
}
```

