# CreateEdgeDriver

调用该接口创建驱动。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateEdgeDriver&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateEdgeDriver|系统规定参数。取值：CreateEdgeDriver。 |
|DriverName|String|是|MyLedDriver|驱动名称。支持大小写英文字母、数字和下划线（\_），必须以英文字母开头，不超过20个字符。 |
|DriverProtocol|String|是|customize|驱动通信协议。取值如下：

 -   modbus：Modbus通信协议。
-   opc-ua：OPC UA通信协议。
-   customize：自定义通信协议。 |
|Runtime|String|是|c|驱动的语言类型。支持如下三种类型：

 -   nodejs8：Node.js v8
-   python3：Python v3.5
-   c: C语言 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |
|CpuArch|String|否|x86-64|驱动适配的CPU架构。取值如下：

 -   armv7
-   armv7-hf
-   aarch64
-   x86-64
-   x86 |
|IsBuiltIn|Boolean|否|false|是否内置驱动文件。

 -   true：表示驱动为内置驱动，即驱动代码已预置到网关上。
-   false：表示驱动为非内置驱动。 非内置驱动必须上传驱动代码。默认为false。

**说明：** 非内置驱动必须上传驱动代码。如需通过API的方式上传驱动代码并获取阿里云对象存储（OSS）地址，请调用[CreateOssPreSignedAddress](~~155858~~)接口创建预签名地址后，使用OSS SDK上传驱动文件。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|DriverId|String|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|BB179FE4-94AB-41B0-AE8A-66DDB7B8B13A|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeDriver
&DriverProtocol=customize
&Runtime=c
&DriverName=MyLedDriver
&CpuArch=x86-64
&IsBuiltIn=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateEdgeDriverResponse>
      <DriverId>fec565038d7544978d9aed5c1a******</DriverId>
      <RequestId>BB179FE4-94AB-41B0-AE8A-66DDB7B8B13A</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</CreateEdgeDriverResponse>
```

`JSON` 格式

```
{
  "DriverId": "fec565038d7544978d9aed5c1a******",
  "RequestId": "BB179FE4-94AB-41B0-AE8A-66DDB7B8B13A",
  "Code": "Success",
  "Success": true
}
```

