# DeleteEdgeInstanceMessageRouting

调用该接口删除边缘实例中的消息路由。

## 限制条件

-   如果在企业版实例中调用该接口，必须传入参数**IotInstanceId**的值。否则，调用接口会失败。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteEdgeInstanceMessageRouting&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteEdgeInstanceMessageRouting|系统规定参数。取值：DeleteEdgeInstanceMessageRouting。 |
|InstanceId|String|是|5zvK1COK1gtr\*\*\*\*\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标指针悬浮在目标边缘实例名称上获取ID。 |
|RouteId|Long|是|123456|消息路由的ID。您可以调用[QueryEdgeInstanceMessageRouting](~~212633~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|物联网平台的实例ID：

 -   企业版实例：必须传入此参数。您可在[物联网平台控制台](http://iot.console.aliyun.com/)的**实例概览**页面，查看您的企业版实例ID。
-   公共实例：无需传入此参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码：

 -   **Success**：表示成功。
-   其它：表示错误码。错误码详情，请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|E252BC84-EF9A-4F0F-8E73-ADCF9CA3B722|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功：

 -   **true**：表示调用成功。
-   **false**：表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=DeleteEdgeInstanceMessageRouting
&instanceId=5zvK1COK1gtr********
&routeId=123456
&regionId=cn-shanghai
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteEdgeInstanceMessageRoutingResponse>
    <code>Success</code>
    <requestId>E252BC84-EF9A-4F0F-8E73-ADCF9CA3B722</requestId>
    <success>true</success>
</DeleteEdgeInstanceMessageRoutingResponse>
```

`JSON`格式

```
{
  "code": "Success",
  "requestId": "E252BC84-EF9A-4F0F-8E73-ADCF9CA3B722",
  "success": true
}
```

