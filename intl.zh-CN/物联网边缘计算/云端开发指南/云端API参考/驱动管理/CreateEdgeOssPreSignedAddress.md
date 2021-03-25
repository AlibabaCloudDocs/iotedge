# CreateEdgeOssPreSignedAddress

调用该接口创建对象存储（OSS）预签名地址。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateEdgeOssPreSignedAddress&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateEdgeOssPreSignedAddress|系统规定参数。取值：CreateEdgeOssPreSignedAddress。 |
|FileName|String|是|testfile.zip|文件名，格式为`<文件名>.<后缀>`。 |
|ResourceId|String|是|df9b9f441\*\*\*\*\*\*\*\*\*4c90d0c21d14|资源ID。目前仅支持驱动资源，因此此处为驱动ID。

 可在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**驱动管理**页面中，鼠标悬浮在目标驱动名称上获取驱动ID。您也可以调用[QueryEdgeDriver](~~155776~~)接口获取驱动ID。 |
|ResourceVersion|String|是|2.0.0|资源版本。目前仅支持驱动资源，因此此处为驱动版本。 |
|Type|String|是|DRIVER\_VERSION\_CONTENT|文件内容类型。有如下三种类型：

 -   DRIVER\_VERSION\_CONTENT：驱动某一版本的代码。
-   DRIVER\_VERSION\_DEFAULT\_CONFIG：驱动某一版本的默认配置。
-   INSTANCE\_DRIVER\_VERSION\_CONFIG：边缘实例驱动某一版本的配置。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|InstanceId|String|否|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。

 **说明：** 当**Type**参数取值为**INSTANCE\_DRIVER\_VERSION\_CONFIG**时，此项不可为空。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|OssAddress|String|http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81\*\*\*\*\*\*\*8fe7da0/DRIVER\_VERSION\_CONTENT/df9b9f441\*\*\*\*\*\*\*\*\*4c90d0c21d14/2.0.0/1581586102750/driver\_code.zip|OSS地址。 |
|OssPreSignedAddress|String|http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81\*\*\*\*\*\*\*8fe7da0/DRIVER\_VERSION\_CONTENT/df9b9f441\*\*\*\*\*\*\*\*\*4c90d0c21d14/2.0.0/1581586102750/driver\_code.zip?Expires\\u003d1581586402\\u0026OSSAccessKeyId\\u003daS4MT0IYrP\*\*\*\*\*\*\\u0026Signature\\u003dIUUjZ881H3rUoCOwjMXPmGbw\*\*\*\*\*\*|OSS预签名地址。更多信息，请参见[OSS文档](~~32016~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|91E2BFA2-ECD7-4E11-B36B-66BCC4773922|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeOssPreSignedAddress
&Type=DRIVER_VERSION_CONTENT
&ResourceId=df9b9f441*********4c90d0c21d14
&FileName=driver_code.zip
&ResourceVersion=2.0.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateEdgeOssPreSignedAddressResponse>
    <RequestId>91E2BFA2-ECD7-4E11-B36B-66BCC4773922</RequestId>
    <Data>
        <OssPreSignedAddress>http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81*******8fe7da0/DRIVER_VERSION_CONTENT/df9b9f441*********4c90d0c21d14/2.0.0/1581586102750/driver_code.zip?Expires=1581586402&amp;OSSAccessKeyId=aS4MT0IYrP******&amp;Signature=IUUjZ881H3rUoCOwjMXPmGbw******</OssPreSignedAddress>
        <OssAddress>http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81*******8fe7da0/DRIVER_VERSION_CONTENT/df9b9f441*********4c90d0c21d14/2.0.0/1581586102750/driver_code.zip</OssAddress>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</CreateEdgeOssPreSignedAddressResponse>
```

`JSON` 格式

```
{
  "RequestId": "91E2BFA2-ECD7-4E11-B36B-66BCC4773922",
  "Data": {
    "OssPreSignedAddress": "http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81*******8fe7da0/DRIVER_VERSION_CONTENT/df9b9f441*********4c90d0c21d14/2.0.0/1581586102750/driver_code.zip?Expires\u003d1581586402\u0026OSSAccessKeyId\u003daS4MT0IYrP******\u0026Signature\u003dIUUjZ881H3rUoCOwjMXPmGbw******",
    "OssAddress": "http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81*******8fe7da0/DRIVER_VERSION_CONTENT/df9b9f441*********4c90d0c21d14/2.0.0/1581586102750/driver_code.zip"
  },
  "Code": "Success",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

