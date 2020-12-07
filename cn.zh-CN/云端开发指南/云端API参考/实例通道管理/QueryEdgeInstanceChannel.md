# QueryEdgeInstanceChannel

调用该接口查询边缘实例中的驱动通道列表。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceChannel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceChannel|系统规定参数。取值：QueryEdgeInstanceChannel。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|DriverId|String|是|9c1ae7bd59f1469abbdccc9592\*\*\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|InstanceId|String|是|6GaTtvTj7vJhiS\*\*\*\*\*\*|边缘实例的ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|PageSize|Integer|是|15|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ChannelName|String|否|le\_name0|驱动通道名称。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时返回的数据。 |
|ChannelList|Array of Channel| |驱动通道信息列表。 |
|Channel| | | |
|ChannelId|String|BE0BD49EF5EF4D119D09CC1B25\*\*\*\*\*\*|驱动通道ID。 |
|ChannelName|String|le\_name0|驱动通道名称。 |
|ConfigList|Array of Config| |配置信息列表。 |
|Config| | | |
|ConfigId|String|5d6016035c1a451daf174b1051\*\*\*\*\*\*|配置ID。 |
|Content|String|\{\\"protocol\\":\\"TCP\\", \\"ip\\":\\"1.2.3.4\\", \\"port\\":1\}|配置内容。 |
|Format|String|JSON|配置格式。取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。 |
|Key|String|key1|配置的关键字。 |
|GmtCreate|String|2020-03-16 23:06:52|创建驱动通道的时间。 |
|GmtCreateTimestamp|Long|1584371212000|创建驱动通道的Unix时间戳。 |
|GmtModified|String|2020-03-16 23:06:52|最后一次更新驱动通道的时间。 |
|GmtModifiedTimestamp|Long|1584371212000|最后一次更新驱动通道的Unix时间戳。 |
|CurrentPage|Integer|1|当前页码。 |
|PageSize|Integer|15|返回结果中每页显示的记录数量。 |
|Total|Integer|1|驱动通道总数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|AA1EF007-0455-43C7-8E03-39D0BA20F4F5|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceChannel
&DriverId=9c1ae7bd59f1469abbdccc9592******
&PageSize=15
&InstanceId=6GaTtvTj7vJhiS******
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryEdgeInstanceChannelResponse>
    <RequestId>AA1EF007-0455-43C7-8E03-39D0BA20F4F5</RequestId>
    <Data>
        <PageSize>15</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>1</Total>
        <ChannelList>
            <Channel>
                <GmtCreate>2020-03-16 23:06:52</GmtCreate>
                <ChannelName>le_name0</ChannelName>
                <GmtCreateTimestamp>1584371212000</GmtCreateTimestamp>
                <GmtModified>2020-03-16 23:06:52</GmtModified>
                <GmtModifiedTimestamp>1584371212000</GmtModifiedTimestamp>
                <ChannelId>BE0BD49EF5EF4D119D09CC1B25******</ChannelId>
                <ConfigList>
                    <Config>
                        <Format>JSON</Format>
                        <Content>{"protocol":"TCP", "ip":"1.2.3.4", "port":1}</Content>
                        <ConfigId>5d6016035c1a451daf174b1051******</ConfigId>
                    </Config>
                </ConfigList>
            </Channel>
        </ChannelList>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceChannelResponse>
```

`JSON` 格式

```
{
  "RequestId": "AA1EF007-0455-43C7-8E03-39D0BA20F4F5",
  "Data": {
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 1,
    "ChannelList": {
      "Channel": [
        {
          "GmtCreate": "2020-03-16 23:06:52",
          "ChannelName": "le_name0",
          "GmtCreateTimestamp": 1584371212000,
          "GmtModified": "2020-03-16 23:06:52",
          "GmtModifiedTimestamp": 1584371212000,
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
    }
  },
  "Code": "Success",
  "Success": true
}
```

