# DeleteEdgeDriverVersion

调用该接口删除驱动的某一版本。

## 限制条件

-   已发布的驱动版本，不允许删除。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteEdgeDriverVersion&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteEdgeDriverVersion|系统规定参数。取值：DeleteEdgeDriverVersion。 |
|DriverId|String|是|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|DriverVersion|String|是|1.2.0|驱动版本号。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|J82E857F-T6B9-4FDE-96B8-E4BE97095D1A|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=DeleteEdgeDriverVersion
&DriverId=fec565038d7544978d9aed5c1a******
&DriverVersion=1.2.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteEdgeDriverVersionResponse>
      <RequestId>J82E857F-T6B9-4FDE-96B8-E4BE97095D1A</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</DeleteEdgeDriverVersionResponse>
```

`JSON` 格式

```
{
  "RequestId": "J82E857F-T6B9-4FDE-96B8-E4BE97095D1A",
  "Code": "Success",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

