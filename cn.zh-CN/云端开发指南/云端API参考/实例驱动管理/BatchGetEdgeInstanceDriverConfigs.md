# BatchGetEdgeInstanceDriverConfigs

调用该接口批量获取边缘实例驱动配置。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchGetEdgeInstanceDriverConfigs&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchGetEdgeInstanceDriverConfigs|系统规定参数。取值：BatchGetEdgeInstanceDriverConfigs。 |
|DriverIds.N|RepeatList|是|021d154d2a2f4dd7a489773d9e04\*\*\*\*|要查询的驱动ID列表。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。

 **说明：** 最多可传入20个驱动ID，即最多可批量获取20个驱动的配置。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|DriverConfigList|Array of DriverConfig| |调用成功时，返回的数据。 |
|ConfigList|Array of Config| |驱动配置信息。 |
|ConfigId|String|dac71722ceac4a299dbf3e8dc3c8\*\*\*\*|配置ID。 |
|Content|String|\{\\"test\\":123\}|配置内容文本或存储配置内容文件的OSS地址。 |
|Format|String|JSON|配置文件格式，取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。 |
|Key|String|key1|配置的关键字。在有多个配置的情况下，用于区分配置。 |
|DriverId|String|021d154d2a2f4dd7a489773d9e04\*\*\*\*|驱动ID。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|D6113390-F507-458B-8544-7B01F945630B|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetEdgeInstanceDriverConfigs
&DriverIds.1=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchGetEdgeInstanceDriverConfigsResponse>
    <DriverConfigList>
        <DriverConfig>
            <DriverId>021d154d2a2f4dd7a489773d9e0****c</DriverId>
            <ConfigList>
                <Config>
                    <Format>JSON</Format>
                    <Content>{"test":123}</Content>
                    <ConfigId>dac71722ceac4a299dbf3e8dc3c8****</ConfigId>
                </Config>
            </ConfigList>
        </DriverConfig>
    </DriverConfigList>
    <RequestId>D6113390-F507-458B-8544-7B01F945630B</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</BatchGetEdgeInstanceDriverConfigsResponse>
```

`JSON` 格式

```
{
  "DriverConfigList": [
    {
      "DriverId": "021d154d2a2f4dd7a489773d9e04****",
      "ConfigList": [
        {
          "Format": "JSON",
          "Content": "{\"test\":123}",
          "ConfigId": "dac71722ceac4a299dbf3e8dc3c8****"
        }
      ]
    }
  ],
  "RequestId": "D6113390-F507-458B-8544-7B01F945630B",
  "Code": "Success",
  "Success": true
}
```

