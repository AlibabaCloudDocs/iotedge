# BindGatewayToEdgeInstance

调用该接口将网关分配到边缘实例中。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BindGatewayToEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BindGatewayToEdgeInstance|系统规定参数。取值：BindGatewayToEdgeInstance。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1mAdeG\*\*\*\*|网关所属产品的Key，产品的唯一标识符。

 **说明：** 如果传入此参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|device1|网关设备名称。

 **说明：** 如果传入此参数，需同时传入**ProductKey**。 |
|IotId|String|否|4z819VQHk6VSLmmBJfrf0010\*\*\*\*\*\*|网关设备的ID，物联网平台为设备生成的唯一标识符，与**ProductKey**和**DeviceName**组合一一对应。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**；如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|28D159F4-980F-423D-95F0-F705E9DFC016|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BindGatewayToEdgeInstance
&InstanceId=F3APY0tPLhmgGtx0****
&ProductKey=a1mAdeG****
&DeviceName=e46ea1a4347c42a0a83b8c956ab1ab
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BindGatewayToEdgeInstanceResponse>
      <RequestId>E3817065-2A17-4814-82FA-66FAB2CC01DF</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</BindGatewayToEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "E3817065-2A17-4814-82FA-66FAB2CC01DF",
  "Code": "Success",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

