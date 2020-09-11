# QueryEdgeInstanceGateway

调用该接口查询边缘实例中的网关。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** 子账号共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceGateway&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceGateway|系统规定参数。取值：QueryEdgeInstanceGateway。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在物联网平台控制台的**边缘计算** \> **边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|GatewayList|Array of Gateway| |调用成功时，返回的网关数据。 |
|DeviceName|String|gateway\_01|网关设备名称。 |
|EdgeVersion|String|v1.0.0|边缘服务版本号。 |
|IotId|String|LuD9x5hiRUdVemWU\*\*\*\*000101|网关设备的ID，物联网平台为设备生成的唯一标识符。 |
|ProductKey|String|a1mAdeG\*\*\*\*|网关所属产品的Key，产品的唯一标识符。 |
|RequestId|String|28D159F4-980F-423D-95F0-F705E9DFC016|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceGateway
&InstanceId=F3APY0tPLhmgGtx0****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryEdgeInstanceGatewayResponse>
    <GatewayList>
        <Gateway>
            <IotId>LuD9x5hiRUdVemWU****000101</IotId>
            <ProductKey>a1mAdeG****</ProductKey>
            <DeviceName>gateway_01</DeviceName>
            <EdgeVersion>v1.0.0</EdgeVersion>
        </Gateway>
    </GatewayList>
    <RequestId>547A62E5-0D6D-4DB5-9CCC-58C706891976</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceGatewayResponse>
```

`JSON` 格式

```
{
  "GatewayList": [
    {
      "IotId": "LuD9x5hiRUdVemWU****000101",
      "ProductKey": "a1mAdeG****",
      "DeviceName": "gateway_01",
      "EdgeVersion": "v1.0.0"
    }
  ],
  "RequestId": "547A62E5-0D6D-4DB5-9CCC-58C706891976",
  "Code": "Success",
  "Success": true
}
```

