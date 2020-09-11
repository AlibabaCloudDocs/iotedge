# ReplaceEdgeInstanceGateway

调用该接口，替换已绑定到边缘实例的网关。替换网关后，原网关的部署状态和部署历史会被清除。

## 限制条件

-   替换网关前，必须先在物联网平台控制台的**边缘计算** \> **边缘实例**\> **实例详情**页面重置边缘实例。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** 子账号共享主账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ReplaceEdgeInstanceGateway&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReplaceEdgeInstanceGateway|系统规定参数。取值：ReplaceEdgeInstanceGateway。 |
|CurrentGatewayId|String|是|oTCJomvT95WPyPPQ5sje\*\*\*\*\*\*|当前网关设备的IotId。IotId是物联网平台为设备生成的唯一标识符。可调用[QueryDevice](~~69905~~)接口查询。 |
|InstanceId|String|是|G4TGWGYwpo8zwr\*\*\*\*\*\*|边缘实例的ID。在物联网平台控制台的**边缘计算** \> **边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|NewGatewayId|String|是|65SkFyhZcU5d3PO2Ri13\*\*\*\*\*\*|要替换的新网关设备的IotId。IotId是物联网平台为设备生成的唯一标识符。可调用[QueryDevice](~~69905~~)接口查询。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|10E5C856-E0A1-4468-BE01-E540A8BA8819|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=ReplaceEdgeInstanceGateway
&CurrentGatewayId=oTCJomvT95WPyPPQ5sje******
&InstanceId=G4TGWGYwpo8zwr******
&NewGatewayId=65SkFyhZcU5d3PO2Ri13******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ReplaceEdgeInstanceGatewayResponse>
    <RequestId>10E5C856-E0A1-4468-BE01-E540A8BA8819</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</ReplaceEdgeInstanceGatewayResponse>
```

`JSON` 格式

```
{
  "RequestId": "10E5C856-E0A1-4468-BE01-E540A8BA8819",
  "Code": "Success",
  "Success": true
}
```

