# QueryEdgeDriverVersion

调用该接口分页查询驱动版本列表。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeDriverVersion&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeDriverVersion|系统规定参数。取值：QueryEdgeDriverVersion。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|DriverId|String|是|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取ID。

 您也可以调用[QueryEdgeDriver](~~155776~~)接口获取。 |
|PageSize|Integer|是|15|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DriverVersion|String|否|led驱动|驱动版本号。设置该参数表示仅查询该版本号匹配的驱动版本信息。 |
|VersionState|Integer|否|0|驱动版本状态。

 -   0：表示查询未发布的驱动版本。
-   1：表示查询已发布的驱动版本。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|DriverVersionList|Array of DriverVersion| |驱动版本列表。 |
|Argument|String|-XX:+PrintGCDetails|JVM（Java Virtual Machine）启动参数。 |
|ConfigCheckRule|String|\{\\"deviceConfig\\":\{\\"required\\":false\},\\"driverConfig\\":\{\\"required\\":false\}\}|配置校验规则。JSON格式字符串，格式如下：

 `{"deviceConfig":{"required":false},"driverConfig":{"required":false}` 参数说明如下。

 -   driverConfig：表示边缘实例中该驱动的配置校验规则。
-   deviceConfig：表示边缘实例中该驱动下设备的配置校验规则。 |
|ContainerConfig|String|\{\\"devMappings\\":\[\],\\"hostNetworkMode\\":0,\\"portMappings\\":\[\],\\"privileged\\":1,\\"volumeMappings\\":\[\]\}|容器配置。JSON格式字符串参数说明，请参见本文下方ContainerConfig表格。 |
|Description|String|Led驱动|驱动描述。 |
|DriverConfig|String|\[\{\\"content\\":\\"\{\\\\\\"defaultConfig\\\\\\":\\\\\\"this is default driver config demo\\\\\\"\}\\",\\"format\\":\\"JSON\\"\}\]|驱动配置。JSON格式字符串，格式如下：

 `{"format":"JSON","content":"{}"}` 参数说明如下所示。

 -   format：配置格式。取值有KV（键值对配置）、JSON（JSON格式）、FILE（配置文件）。
-   content：配置内容。format为KV或JSON时，此处为配置内容；format为FILE时，此处为OSS地址。 |
|DriverId|String|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|驱动ID。 |
|DriverVersion|String|1.2.0|驱动版本号。 |
|EdgeVersion|String|2.0.0|驱动适配的边缘版本。 |
|GmtCreateTimestamp|Long|1581912859713|创建驱动的Unix时间戳。 |
|GmtModifiedTimestamp|Long|1581912859713|最后一次更新驱动的Unix时间戳。 |
|SourceConfig|String|\{\\"ossAddress\\":\\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3\*\*\*\*\*\*/ck3n3koe200003h6zf\*\*\*\*\*\*.zip\\",\\"temporaryOssAddress\\":\\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3\*\*\*\*\*\*/ck3n3koe200003h6zf\*\*\*\*\*\*.zip?Expires\\u003d1575\*\*\*\*\*\*\\u0026OSSAccessKeyId\\u003daS4MT0IYr\*\*\*\*\*\*\\u0026Signature\\u003dm6cpmcaB8rm3YfbkhTYgb0W\*\*\*\*\*\*\\"\}|驱动代码来源配置。JSON格式字符串，格式如下：

 `{"ossAddress":"http://***/driver_code.zip","temporaryOssAddress":"http://***/driver_code.zip?Expires***"}` 其中，`ossAddress`为对象存储（OSS）访问地址，`temporaryOssAddress`为可以直接下载的临时链接，有效期5分钟。 |
|VersionState|String|0|驱动版本状态。

 -   0：表示该版本未发布。
-   1：表示该版本已发布。 |
|PageSize|Integer|15|返回结果中每页显示的记录数量。 |
|Total|Integer|1|驱动数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|ABA0CD1F-4270-42FE-84AD-D612240196F7|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

**ContainerConfig参数说明**

|名称

|类型

|描述 |
|----|----|----|
|privileged

|Integer

|是否启动特权模式。

 0：表示否。

 1：表示是。 |
|hostNetworkMode

|Integer

|是否使用宿主机host模式。

 0：表示否。

 1：表示是。 |
|portMappings

|List

|网络端口映射。格式请参考本文下方portMappings表格。 |
|devMappings

|List

|设备映射。格式请参考本文下方devMappings表格。 |
|volumeMappings

|List

|卷映射。格式请参考本文下方volumeMappings表格。 |

**portMappings参数说明**

|名称

|类型

|描述 |
|----|----|----|
|hostPort

|Integer

|宿主机端口。 |
|containerPort

|Integer

|容器内端口。 |
|protocol

|Integer

|协议类型。取值有tcp和udp两种。 |

**devMappings参数说明**

|名称

|类型

|描述 |
|----|----|----|
|hostPath

|String

|设备名称。 |
|permission

|String

|读写权限。

 ro：只读权限。

 rw：读写权限。 |
|comment

|String

|注释信息。 |

**volumeMappings参数说明**

|名称

|类型

|描述 |
|----|----|----|
|hostPath

|String

|源路径。 |
|containerPath

|String

|目的路径。 |
|permission

|String

|读写权限。

 ro：只读权限。

 rw：读写权限。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeDriverVersion
&DriverId=fec565038d7544978d9aed5c1a******
&PageSize=15
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryEdgeDriverVersionResponse>
      <RequestId>ABA0CD1F-4270-42FE-84AD-D612240196F7</RequestId>
      <Data>
            <PageSize>15</PageSize>
            <CurrentPage>1</CurrentPage>
            <Total>1</Total>
            <DriverVersionList>
                  <DriverVersion>
                        <ContainerConfig>{"devMappings":[],"hostNetworkMode":0,"portMappings":[],"privileged":1,"volumeMappings":[]}</ContainerConfig>
                        <GmtCreate>2019-12-01 22:28:01</GmtCreate>
                        <DriverId>fec565038d7544978d9aed5c1a******</DriverId>
                        <Description>Led驱动</Description>
                        <DriverVersion>1.2.0</DriverVersion>
                        <SourceConfig>{"ossAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30******/ck3n3koe200003h6zf******.zip","temporaryOssAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30******/ck3n3koe200003h6zf******.zip?Expires=1575******&amp;OSSAccessKeyId=aS4MT0IYrPS******&amp;Signature=m6cpmcaB8rm3YfbkhTYgb0WO******"}</SourceConfig>
                        <GmtModified>2019-12-01 22:28:01</GmtModified>
                        <DriverConfig>[{"content":"{\"defaultConfig\":\"this is default driver config demo\"}","format":"JSON"}]</DriverConfig>
                        <EdgeVersion>2.0.0</EdgeVersion>
                        <ConfigCheckRule>{"deviceConfig":{"required":false},"driverConfig":{"required":false}}</ConfigCheckRule>
                        <VersionState>0</VersionState>
                  </DriverVersion>
            </DriverVersionList>
      </Data>
      <Code>Success</Code>
      <Success>true</Success>
</QueryEdgeDriverVersionResponse>
```

`JSON` 格式

```
{
  "RequestId": "ABA0CD1F-4270-42FE-84AD-D612240196F7",
  "Data": {
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 1,
    "DriverVersionList": [
      {
        "ContainerConfig": "{\"devMappings\":[],\"hostNetworkMode\":0,\"portMappings\":[],\"privileged\":1,\"volumeMappings\":[]}",
        "GmtCreate": "2019-12-01 22:28:01",
        "DriverId": "fec565038d7544978d9aed5c1a******",
        "Description": "Led驱动",
        "DriverVersion": "1.2.0",
        "SourceConfig": "{\"ossAddress\":\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3******/ck3n3koe200003h6zf******.zip\",\"temporaryOssAddress\":\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3******/ck3n3koe200003h6zf******.zip?Expires\u003d1575******\u0026OSSAccessKeyId\u003daS4MT0IYr******\u0026Signature\u003dm6cpmcaB8rm3YfbkhTYgb0W******\"}",
        "GmtModified": "2019-12-01 22:28:01",
        "DriverConfig": "[{\"content\":\"{\\\"defaultConfig\\\":\\\"this is default driver config demo\\\"}\",\"format\":\"JSON\"}]",
        "EdgeVersion": "2.0.0",
        "ConfigCheckRule": "{\"deviceConfig\":{\"required\":false},\"driverConfig\":{\"required\":false}}",
        "VersionState": 0
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

