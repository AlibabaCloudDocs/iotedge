# UpdateEdgeDriverVersion

调用该接口更新驱动版本。

## 限制条件

-   请求参数中置空的参数（不填写参数值），将清空原来的参数值配置。
-   已发布的驱动版本，不允许更新。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** 子账号共享主账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateEdgeDriverVersion&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateEdgeDriverVersion|系统规定参数。取值：UpdateEdgeDriverVersion。 |
|DriverId|String|是|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。在物联网平台控制台的**边缘计算** \> **驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|DriverVersion|String|是|1.2.0|驱动版本号。 |
|EdgeVersion|String|是|2.0.0|驱动适配的边缘版本，即该驱动只能在该边缘版本及以上版本的网关中运行。例如2.4.0，表示在v2.4.0及以上的边缘版本中运行该驱动。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |
|Description|String|否|Led驱动（更新描述）|驱动描述。长度不超过256个字节。 |
|SourceConfig|String|否|\{"ossAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30c\*\*\*\*\*\*/ck3n3koe200003h6zf\*\*\*\*\*\*.zip"\}|驱动代码来源配置。JSON格式字符串，格式如下：

 `{"ossAddress":"http://***/driver_code.zip"}` 其中，`ossAddress`为对象存储（OSS）访问地址，如需通过API的方式上传驱动代码并获取OSS地址，请调用[CreateOssPreSignedAddress](~~155858~~)接口获取。 |
|DriverConfig|String|否|\[\{"format":"JSON","content":"\{\\"defaultConfig\\":\\"this is default driver config demo\\"\}"\}\]|驱动配置。JSON格式字符串，格式如下：

 `{"format":"JSON","content":"{}"}` 参数说明如下所示。

 -   format：配置格式。取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。
-   content：配置内容。format为KV或JSON时，请填配置内容；format为FILE时，请填OSS地址。

**说明：** OSS地址请调用[CreateOssPreSignedAddress](~~155858~~)接口获取。 |
|ContainerConfig|String|否|\{"privileged":1,"devMappings":\[\],"volumeMappings":\[\],"hostNetworkMode":0,"portMappings":\[\]\}|容器配置。JSON格式字符串。详情请参见本文下方ContainerConfig表格。 |
|ConfigCheckRule|String|否|\{"deviceConfig":\{"required":false\},"driverConfig":\{"required":false\}\}|配置校验规则。JSON格式字符串，格式如下：

 `{"deviceConfig":{"required":false},"driverConfig":{"required":false}` 参数说明如下。

 -   driverConfig：表示边缘实例中该驱动的配置校验规则。
-   deviceConfig：表示边缘实例中该驱动下设备的配置校验规则。

 `required`为true表示参数不能为空；false表示参数允许为空。 |
|Argument|String|否|-XX:+PrintGCDetails|JVM（Java Virtual Machine）启动参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

**ContainerConfig参数说明**

|名称

|类型

|是否必需

|描述 |
|----|----|------|----|
|privileged

|Integer

|否

|是否启动特权模式。

 0：表示否。

 1：表示是。 |
|hostNetworkMode

|Integer

|否

|是否使用宿主机host模式。

 0：表示否。

 1：表示是。 |
|portMappings

|List

|否

|网络端口映射。使用宿主机host模式时无须配置此项。最多可添加10个网络端口映射。格式请参考本文下方portMappings表格。 |
|devMappings

|List

|否

|设备映射。使用特权模式时无须配置此项。最多可添加10个设备映射。格式请参考本文下方devMappings表格。 |
|volumeMappings

|List

|否

|卷映射。最多可添加10个卷映射。格式请参考本文下方volumeMappings表格。 |

**portMappings参数说明**

|名称

|类型

|是否必需

|描述 |
|----|----|------|----|
|hostPort

|Integer

|是

|宿主机端口。端⼝取值范围为1～65535。 |
|containerPort

|Integer

|是

|容器内端口。端⼝取值范围为1～65535。 |
|protocol

|Integer

|是

|协议类型。取值有tcp和udp两种。 |

**devMappings参数说明**

|名称

|类型

|是否必需

|描述 |
|----|----|------|----|
|hostPath

|String

|是

|设备名称。需要以

`/dev/`开头，长度为1~128个字符。 |
|permission

|String

|是

|读写权限。

 ro：只读权限。

 rw：读写权限。 |
|comment

|String

|否

|注释信息。长度为1~128个字符。 |

**volumeMappings参数说明**

|名称

|类型

|是否必需

|描述 |
|----|----|------|----|
|hostPath

|String

|是

|源路径。长度为1~128个字符，不支持空格。 |
|containerPath

|String

|是

|目的路径。须填写绝对路径，不支持根目录，以

`/`开头，长度为2~128个字符，不支持空格。 |
|permission

|String

|是

|读写权限。

 ro：只读权限。

 rw：读写权限。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|7757A782-6C24-4325-A663-C62857F32E87|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=UpdateEdgeDriverVersion
&DriverId=fec565038d7544978d9aed5c1a******
&Description=Led驱动（更新描述）
&DriverVersion=1.2.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateEdgeDriverVersionResponse>
      <RequestId>7757A782-6C24-4325-A663-C62857F32E87</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</UpdateEdgeDriverVersionResponse>
```

`JSON` 格式

```
{
  "RequestId": "7757A782-6C24-4325-A663-C62857F32E87",
  "Code": "Success",
  "Success": true
}
```

