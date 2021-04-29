# CreateEdgeInstanceMessageRouting

调用该接口，为指定的边缘实例创建消息路由。

## 限制条件

-   如果在企业版实例中调用该接口，必须传入参数**IotInstanceId**的值。否则，调用接口会失败。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateEdgeInstanceMessageRouting&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateEdgeInstanceMessageRouting|系统规定参数。取值：CreateEdgeInstanceMessageRouting。 |
|InstanceId|String|是|nF9oXo7kLRWQ\*\*\*\*\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标指针悬浮在目标边缘实例名称上获取ID。 |
|SourceType|String|是|device|消息来源，取值如下：

 -   **device**：表示消息由设备发出。
-   **function**：表示消息由边缘应用发出。
-   **IotHub**：表示消息由云端发出。 |
|TargetType|String|是|function|消息接收者，取值分如下几种情况：

 -   **SourceType**取值为**device**时：该参数可取的值为**function**或**IotHub**，表示由设备发出的消息，传给边缘应用或云端。
-   **SourceType**取值为**function**时：该参数可取的值为**function**或**IotHub**，表示由边缘应用发出的消息，传给另一个边缘应用或云端。
-   **SourceType**取值为**IotHub**时：该参数可取的值为**function**，表示由云端发出的消息，传给边缘应用。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|物联网平台的实例ID：

 -   企业版实例：必须传入此参数。您可在[物联网平台控制台](http://iot.console.aliyun.com/)的**实例概览**页面，查看您的企业版实例ID。
-   公共实例：无需传入此参数。 |
|Name|String|否|le\_lite2|消息路由名称。长度限制为4~32个字符，汉字和全角符号算2个字符。 |
|TopicFilter|String|否|all|消息过滤条件，取值如下：

 -   具体消息Topic：表示来自消息源，且符合该消息Topic的消息，会被传给消息接收者。Topic相关信息，请参见[什么是Topic](~~73731~~)。
-   **all**：表示来自消息源的所有消息，都会被传给消息接收者。 |
|SourceData|String|否|\#|消息来源的数据，取值分如下几种情况：

 -   **SourceType**取值为**device**时：
    -   如果由指定产品下的指定设备发送消息，则此处取值格式为`/{Your_ProductKey}/{Your_DeviceName}`。

**说明：** 请将\{Your\_ProductKey\}和\{Your\_DeviceName\}替换为您实际设备的ProductKey和DeviceName。

    -   如果由指定产品下的所有设备发送消息，则此处取值格式为`/{Your_ProductKey}/+`。

**说明：** 请将\{Your\_ProductKey\}替换为您实际设备的ProductKey。

    -   如果由边缘实例中所有产品下的所有设备发送消息，则此处取值为`#`。
-   **SourceType**取值为**function**：此处取值为边缘应用的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**应用管理**页面中，鼠标指针悬浮在目标应用名称上获取ID。
-   **SourceType**取值为**IotHub**时：无需传入此参数。 |
|TargetData|String|否|58c46749ac934db3925fe5\*\*\*\*\*\*\*\*|消息接收者的数据，取值分如下几种情况：

 -   **TargetType**取值为**function**时：此处取值为边缘应用的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**应用管理**页面中，鼠标指针悬浮在目标应用名称上获取ID。
-   **TargetType**取值为**IotHub**时：无需传入此参数。 |
|TargetIotHubQos|Integer|否|0|服务级别。取值如下：

 -   **0**：表示消息仅发送一次，不管是否被消息接收者成功接收。
-   **1**：表示最少发送一次消息，直至收到消息接收者的返回信息，则停止发送该消息。

 **说明：** 当**TargetType**为**IoTHub**时，必须传入此参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码：

 -   **Success**：表示成功。
-   其它：表示错误码。错误码详情，请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|AC786033-00C5-4FD6-8435-F2807740D9FA|阿里云为该请求生成的唯一标识符。 |
|RouteId|Long|123456|消息路由的ID。 |
|Success|Boolean|true|是否调用成功：

 -   **true**：表示调用成功。
-   **false**：表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeInstanceMessageRouting
&TargetData=58c46749ac934db3925fe5********
&TopicFilter=all
&InstanceId=nF9oXo7kLRWQ********
&SourceType=device
&TargetType=function
&SourceData=#
&Name=le_lite2
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateEdgeInstanceMessageRoutingResponse>
    <RequestId>BBE0E0C7-913A-47B8-A255-F2C6038B5FD8</RequestId>
    <RouteId>123456</RouteId>
    <Code>Success</Code>
    <Success>true</Success>
</CreateEdgeInstanceMessageRoutingResponse>
```

`JSON`格式

```
{
  "RequestId": "BBE0E0C7-913A-47B8-A255-F2C6038B5FD8",
  "RouteId": 123456,
  "Code": "Success",
  "Success": true
}
```

