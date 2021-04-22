# GetDeviceTunnelShareStatus

调用该接口获取网关隧道的分享状态。

## 限制条件

-   如果在企业版实例中调用该接口，必须传入参数**IotInstanceId**的值。否则，调用接口会失败。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetDeviceTunnelShareStatus&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetDeviceTunnelShareStatus|系统规定参数。取值：GetDeviceTunnelShareStatus。 |
|DeviceName|String|是|LEGatewayAuto\_B3XM\*\*\*\*\*\*|网关的设备名称。 |
|ProductKey|String|是|a1Wmy\*\*\*\*\*\*|网关所属产品的Key，产品的唯一标识符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID：

 -   企业版实例：必须传入此参数。您可在物联网平台控制台的**实例概览**页面，查看您的企业版实例ID。
-   公共实例：无需传入此参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码：

 -   **Success**：表示成功。
-   其它：表示错误码。错误码详情，请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的信息。 |
|GmtOpened|Long|1617941371000|开启隧道分享的Unix时间戳。

 **说明：** 当**IsOpen**的值为**false**时，此处为空。 |
|IsOpen|Boolean|true|是否已开启隧道分享：

 -   **true**：表示已开启。
-   **false**：表示未开启。 |
|Password|String|848bbfa0e9a31e579502869920b4d4c\*\*\*\*\*\*\*\*|隧道分享密码。

 **说明：** 当**IsOpen**的值为**false**时，此处为空。 |
|ShareId|String|18f72f95cad34ca3aeabeeefcb\*\*\*\*\*\*|隧道分享ID。

 **说明：** 当**IsOpen**的值为**false**时，此处为空。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|ACC1D51C-1A58-440E-92A7-71AB61C6595A|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功：

 -   **true**：表示调用成功。
-   **false**：表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=GetDeviceTunnelShareStatus
&ProductKey=a1Wmy******
&DeviceName=LEGatewayAuto_B3XM******
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetDeviceTunnelShareStatusResponse>
    <RequestId>ACC1D51C-1A58-440E-92A7-71AB61C6595A</RequestId>
    <Data>
        <GmtOpened>1617941371000</GmtOpened>
        <ShareId>18f72f95cad34ca3aeabeeefcb******</ShareId>
        <Password>848bbfa0e9a31e579502869920b4d4c********</Password>
        <IsOpen>true</IsOpen>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</GetDeviceTunnelShareStatusResponse>
```

`JSON`格式

```
{
  "RequestId": "ACC1D51C-1A58-440E-92A7-71AB61C6595A",
  "Data": {
    "GmtOpened": 1617941371000,
    "ShareId": "18f72f95cad34ca3aeabeeefcb******",
    "Password": "848bbfa0e9a31e579502869920b4d4c********",
    "IsOpen": true
  },
  "Code": "Success",
  "Success": true
}
```

