# BatchGetDeviceBindStatus

调用该接口批量获取网关或设备绑定到边缘实例的状态。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchGetDeviceBindStatus&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchGetDeviceBindStatus|系统规定参数。取值：BatchGetDeviceBindStatus。 |
|IotIds.N|RepeatList|是|sjI0Sd124XFYyjBYMiYO\*\*\*\*\*\*|设备ID列表。可调用[QueryDevice](~~69905~~)接口查询设备ID。

 **说明：** 单次调用最多可填写20个设备ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Array of DeviceStatus| |调用成功时返回的数据。 |
|BindStatus|Integer|1|网关或设备是否已绑定到边缘实例。

 -   0：表示未绑定。
-   1：表示已绑定。 |
|IotId|String|sjI0Sd124XFYyjBYMiYO\*\*\*\*\*\*|设备ID。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|B1DF865D-2474-4CD5-9B7E-59B06D204CBF|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetDeviceBindStatus
&IotIds.2=BXPV9Ks3bxwM9fDl9Ck0******
&IotIds.1=sjI0Sd124XFYyjBYMiYO******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchGetDeviceBindStatusResponse>
    <RequestId>B1DF865D-2474-4CD5-9B7E-59B06D204CBF</RequestId>
    <Data>
        <DeviceStatus>
            <IotId>sjI0Sd124XFYyjBYMiYO******</IotId>
            <BindStatus>0</BindStatus>
        </DeviceStatus>
        <DeviceStatus>
            <IotId>BXPV9Ks3bxwM9fDl9Ck0******</IotId>
            <BindStatus>1</BindStatus>
        </DeviceStatus>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</BatchGetDeviceBindStatusResponse>
```

`JSON` 格式

```
{
  "RequestId": "B1DF865D-2474-4CD5-9B7E-59B06D204CBF",
  "Data": [
    {
      "IotId": "sjI0Sd124XFYyjBYMiYO******",
      "BindStatus": 0
    },
    {
      "IotId": "BXPV9Ks3bxwM9fDl9Ck0******",
      "BindStatus": 1
    }
  ],
  "Code": "Success",
  "Success": true
}
```

