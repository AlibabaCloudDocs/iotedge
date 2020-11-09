# BatchGetEdgeInstanceDeviceConfig

调用该接口批量获取边缘实例设备配置。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchGetEdgeInstanceDeviceConfig&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchGetEdgeInstanceDeviceConfig|系统规定参数。取值：BatchGetEdgeInstanceDeviceConfig。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotIds.N|RepeatList|是|BXPV9Ks3bxwM9fDl\*\*\*\*000101|要查询的设备ID列表。可调用[QueryEdgeInstanceDevice](~~135261~~)查询实例中的设备ID。

 **说明：** 单次调用最多可填写20个设备ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|DeviceConfigList|Array of DeviceConfig| |调用成功时，返回的设备配置数据。 |
|Config|Struct| |设备配置信息。 |
|Content|String|\{\\"test\\": \\"device\_config\_demo\\"\}|配置内容文本或存储配置内容文件的OSS地址。 |
|Format|String|JSON|配置文件格式。参数值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。 |
|IotId|String|sjI0Sd124XFYyjBY\*\*\*\*000101|设备ID。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|D4A102C2-36A5-4964-9694-0F8EFF95CCA8|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetEdgeInstanceDeviceConfig
&IotIds.2=BXPV9Ks3bxwM9fDl****000101
&IotIds.1=sjI0Sd124XFYyjBY****000101
&InstanceId=F3APY0tPLhmgGtx0****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchGetEdgeInstanceDeviceConfigResponse>
    <DeviceConfigList>
        <DeviceConfig>
            <IotId>sjI0Sd124XFYyjBY****000101</IotId>
            <Config>
                <Format>JSON</Format>
                <Content>{"test": "device_config_demo"}</Content>
            </Config>
        </DeviceConfig>
        <DeviceConfig>
            <IotId>BXPV9Ks3bxwM9fD****0000101</IotId>
            <Config>
                <Format>JSON</Format>
                <Content>{"test": "device_config_demo"}</Content>
            </Config>
        </DeviceConfig>
    </DeviceConfigList>
    <RequestId>D4A102C2-36A5-4964-9694-0F8EFF95CCA8</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</BatchGetEdgeInstanceDeviceConfigResponse>
```

`JSON` 格式

```
{
  "DeviceConfigList": [
    {
      "IotId": "sjI0Sd124XFYyjBY****000101",
      "Config": {
        "Format": "JSON",
        "Content": "{\"test\": \"device_config_demo\"}"
      }
    },
    {
      "IotId": "BXPV9Ks3bxwM9fD****0000101",
      "Config": {
        "Format": "JSON",
        "Content": "{\"test\": \"device_config_demo\"}"
      }
    }
  ],
  "RequestId": "D4A102C2-36A5-4964-9694-0F8EFF95CCA8",
  "Code": "Success",
  "Success": true
}
```

