# BatchGetEdgeDriver

调用该接口批量查询驱动信息。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchGetEdgeDriver&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchGetEdgeDriver|系统规定参数。取值：BatchGetEdgeDriver。 |
|DriverIds.N|RepeatList|是|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID列表。最多可填写30个驱动ID，即一次最多支持查询30个驱动的信息。格式请参见本文下方请求示例。 |
|IotInstanceId|String|否|ot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|DriverList|Array of Driver| |驱动信息列表。 |
|CpuArch|String|x86-64|驱动适配的CPU架构。有如下几种架构：

 -   armv7
-   armv7-hf
-   aarch64
-   x86-64
-   x86 |
|DriverId|String|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。 |
|DriverName|String|MyLedDriver|驱动名称。 |
|DriverProtocol|String|customize|驱动通信协议。

 -   modbus：Modbus通信协议。
-   opc-ua：OPC UA通信协议。
-   customize：自定义通信协议。 |
|GmtCreateTimestamp|Long|1581912859713|创建驱动的Unix时间戳。 |
|GmtModifiedTimestamp|Long|1581912859713|最后一次更新驱动的Unix时间戳。 |
|IsBuiltIn|Boolean|false|驱动文件是否内置。

 -   true：表示驱动为内置驱动，即驱动代码已预置到网关上。
-   false：表示驱动为非内置驱动。 |
|Runtime|String|c|驱动的语言类型。有如下三种类型：

 -   nodejs8：Node.js v8
-   python3：Python v3.5
-   c: C语言 |
|Type|Integer|1|驱动类型。

 -   0：表示官方驱动。
-   1：表示自研驱动。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|A42CAB88-6E26-4DC7-9A35-584D17E82DE0|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetEdgeDriver
&DriverIds.1=fec565038d7544978d9aed5c1a******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchGetEdgeDriverResponse>
      <RequestId>A42CAB88-6E26-4DC7-9A35-584D17E82DE0</RequestId>
      <DriverList>
            <Driver>
                  <DriverProtocol>customize</DriverProtocol>
                  <Type>1</Type>
                  <Runtime>c</Runtime>
                  <GmtCreate>2019-12-01 22:28:00</GmtCreate>
                  <DriverId>fec565038d7544978d9aed5c1a******</DriverId>
                  <DriverName>MyLedDriver</DriverName>
                  <GmtModified>2019-12-01 22:28:00</GmtModified>
                  <IsBuiltIn>false</IsBuiltIn>
                  <CpuArch>x86-64</CpuArch>
            </Driver>
      </DriverList>
      <Code>Success</Code>
      <Success>true</Success>
</BatchGetEdgeDriverResponse>
```

`JSON` 格式

```
{
  "RequestId": "A42CAB88-6E26-4DC7-9A35-584D17E82DE0",
  "DriverList": [
    {
      "DriverProtocol": "customize",
      "Type": 1,
      "Runtime": "c",
      "GmtCreate": "2019-12-01 22:28:00",
      "DriverId": "fec565038d7544978d9aed5c1a******",
      "DriverName": "MyLedDriver",
      "GmtModified": "2019-12-01 22:28:00",
      "IsBuiltIn": false,
      "CpuArch": "x86-64"
    }
  ],
  "Code": "Success",
  "Success": true
}
```

