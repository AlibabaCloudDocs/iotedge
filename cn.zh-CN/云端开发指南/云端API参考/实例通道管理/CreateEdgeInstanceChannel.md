# CreateEdgeInstanceChannel

调用该接口创建边缘实例中的驱动通道。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateEdgeInstanceChannel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateEdgeInstanceChannel|系统规定参数。取值：CreateEdgeInstanceChannel。 |
|ChannelName|String|是|le\_name0|驱动通道名称。支持中文、英文大小写字母、数字和下划线（\_），长度限制1~30个字符。 |
|Configs.N.Content|String|是|\{"protocol":"TCP", "ip":"1.2.3.4", "port":1\}|配置内容。

 -   **Configs.N.Format**参数的值为KV或JSON时，此处请填写配置内容。配置内容格式请参见[驱动通道配置说明](~~172321~~)。
-   **Configs.N.Format**参数的值为FILE时，此处请填写阿里云对象存储OSS地址。OSS地址请调用[CreateOssPreSignedAddress](~~155858~~)接口获取。 |
|Configs.N.Format|String|是|JSON|配置格式。取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。 |
|DriverId|String|是|9c1ae7bd59f1469abbdccc9592\*\*\*\*\*\*|驱动ID。在物联网平台控制台的**边缘计算** \> **驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|6GaTtvTj7vJhiS\*\*\*\*\*\*|边缘实例的ID。在物联网平台控制台的**边缘计算** \> **边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |
|Configs.N.Key|String|否|key1|配置的关键字。在有多个配置的情况下，用于区分配置。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|String|BE0BD49EF5EF4D119D09CC1B25\*\*\*\*\*\*|调用成功时返回的驱动通道ID。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|B34673EA-ECE7-44F5-BF01-40B5FAE633B6|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeInstanceChannel
&Configs.1.Content={"protocol":"TCP", "ip":"1.2.3.4", "port":1}
&DriverId=9c1ae7bd59f1469abbdccc9592******
&ChannelName=le_name0
&InstanceId=6GaTtvTj7vJhiS******
&Configs.1.Format=JSON
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateEdgeInstanceChannelResponse>
    <RequestId>B34673EA-ECE7-44F5-BF01-40B5FAE633B6</RequestId>
    <Data>BE0BD49EF5EF4D119D09CC1B2******</Data>
    <Code>Success</Code>
    <Success>true</Success>
</CreateEdgeInstanceChannelResponse>
```

`JSON` 格式

```
{
  "RequestId": "B34673EA-ECE7-44F5-BF01-40B5FAE633B6",
  "Data": "BE0BD49EF5EF4D119D09CC1B25******",
  "Code": "Success",
  "Success": true
}
```

