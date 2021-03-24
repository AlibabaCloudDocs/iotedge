# SetEdgeInstanceDriverConfigs

调用该接口配置边缘实例驱动。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=SetEdgeInstanceDriverConfigs&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetEdgeInstanceDriverConfigs|系统规定参数。取值：SetEdgeInstanceDriverConfigs。 |
|Configs.N.Content|String|是|\{"test":123\}|配置内容，可以选择传入：

 -   配置内容文本。格式请参见[驱动与设备信息配置](~~120906~~)内容。
-   存储配置文件的阿里云对象存储（OSS）地址。 |
|Configs.N.Format|String|是|JSON|配置文件格式。取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。 |
|DriverId|String|是|021d154d2a2f4dd7a489773d9e04\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Configs.N.Key|String|否|key1|配置的关键字。在有多个配置的情况下，用于区分配置。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|252C7754-F6A2-454B-9DE2-382A97FC0C3F|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=SetEdgeInstanceDriverConfigs
&Configs.1.Content={"test":123}
&DriverId=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&Configs.1.Format=JSON
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetEdgeInstanceDriverConfigsResponse>
      <RequestId>252C7754-F6A2-454B-9DE2-382A97FC0C3F</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</SetEdgeInstanceDriverConfigsResponse>
```

`JSON` 格式

```
{
 "RequestId": "252C7754-F6A2-454B-9DE2-382A97FC0C3F",
 "Code": "Success",
 "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

