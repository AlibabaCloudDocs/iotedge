# BatchGetEdgeInstanceChannel

调用该接口批量查询边缘实例中的驱动通道。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** 子账号共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchGetEdgeInstanceChannel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchGetEdgeInstanceChannel|系统规定参数。取值：BatchGetEdgeInstanceChannel。 |
|ChannelIds.N|RepeatList|是|BE0BD49EF5EF4D119D09CC1B25\*\*\*\*\*\*|驱动通道ID列表。调用[QueryEdgeInstanceChannel](~~162253~~)接口获取通道ID。

 **说明：** 单次调用最多可填写20个通道ID。 |
|DriverId|String|是|9c1ae7bd59f1469abbdccc9592\*\*\*\*\*\*|驱动ID。在物联网平台控制台的**边缘计算** \> **驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|6GaTtvTj7vJhiS\*\*\*\*\*\*|边缘实例的ID。在物联网平台控制台的**边缘计算** \> **边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Array of Channel| |调用成功时返回的数据。 |
|Channel| | | |
|ChannelId|String|BE0BD49EF5EF4D119D09CC1B25\*\*\*\*\*\*|驱动通道ID。 |
|ChannelName|String|le\_name0|驱动通道名称。 |
|ConfigList|Array of Config| |配置信息列表。 |
|Config| | | |
|ConfigId|String|5d6016035c1a451daf174b1051\*\*\*\*\*\*|配置ID。 |
|Content|String|\{\\"protocol\\":\\"TCP\\", \\"ip\\":\\"1.2.3.4\\", \\"port\\":1\}|配置内容。 |
|Format|String|JSON|配置格式。取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。 |
|Key|String|key1|配置的关键字。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|5B86570E-C1A7-4569-BF7B-F7F09EB35BEB|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetEdgeInstanceChannel
&ChannelIds.1=BE0BD49EF5EF4D119D09CC1B25******
&DriverId=9c1ae7bd59f1469abbdccc9592******
&InstanceId=6GaTtvTj7vJhiS******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchGetEdgeInstanceChannelResponse>
    <RequestId>5B86570E-C1A7-4569-BF7B-F7F09EB35BEB</RequestId>
    <Data>
        <Channel>
            <ChannelName>le_name0</ChannelName>
            <ChannelId>BE0BD49EF5EF4D119D09CC1B25******</ChannelId>
            <ConfigList>
                <Config>
                    <Format>JSON</Format>
                    <Content>{"protocol":"TCP", "ip":"1.2.3.4", "port":1}</Content>
                    <ConfigId>5d6016035c1a451daf174b1051******</ConfigId>
                </Config>
            </ConfigList>
        </Channel>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</BatchGetEdgeInstanceChannelResponse>
```

`JSON` 格式

```
{
  "RequestId": "5B86570E-C1A7-4569-BF7B-F7F09EB35BEB",
  "Data": {
    "Channel": [
      {
        "ChannelName": "le_name0",
        "ChannelId": "BE0BD49EF5EF4D119D09CC1B25******",
        "ConfigList": {
          "Config": [
            {
              "Format": "JSON",
              "Content": "{\"protocol\":\"TCP\", \"ip\":\"1.2.3.4\", \"port\":1}",
              "ConfigId": "5d6016035c1a451daf174b1051******"
            }
          ]
        }
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

