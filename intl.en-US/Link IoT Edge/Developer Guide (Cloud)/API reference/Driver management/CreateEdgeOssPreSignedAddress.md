# CreateEdgeOssPreSignedAddress

Creates a pre-signed URL for an object that is stored in Object Storage Service \(OSS\).

## Limits

Each Alibaba Cloud account can run a maximum of five queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateEdgeOssPreSignedAddress&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateEdgeOssPreSignedAddress|The operation that you want to perform. Set the value to CreateEdgeOssPreSignedAddress. |
|FileName|String|Yes|testfile.zip|The name of the object whose URL is to be obtained. The format is `<File name>.<File name extension>`. |
|ResourceId|String|Yes|df9b9f441\*\*\*\*\*\*\*\*\*4c90d0c21d14|The ID of the resource for which the object URL is to be obtained. Only driver resources are supported. Set this parameter to the ID of the corresponding driver.

To obtain the driver ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of the driver for which the object URL you want to obtain and obtain the driver ID. You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver ID. |
|ResourceVersion|String|Yes|2.0.0|The version number of the resource. Only driver resources are supported. Set this parameter to the version number of the corresponding driver. |
|Type|String|Yes|DRIVER\_VERSION\_CONTENT|The content type of the object. Valid values:

-   DRIVER\_VERSION\_CONTENT: the code of a specific driver version.
-   DRIVER\_VERSION\_DEFAULT\_CONFIG: the default configuration of a specific driver version.
-   INSTANCE\_DRIVER\_VERSION\_CONFIG: the configuration of a specific driver version that is used in an edge instance. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|InstanceId|String|No|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that uses the driver and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID.

**Note:** When the **Type** parameter is set to **INSTANCE\_DRIVER\_VERSION\_CONFIG**, this parameter is required. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~135196~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|OssAddress|String|http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81\*\*\*\*\*\*\*8fe7da0/DRIVER\_VERSION\_CONTENT/df9b9f441\*\*\*\*\*\*\*\*\*4c90d0c21d14/2.0.0/1581586102750/driver\_code.zip|The URL of the OSS object. |
|OssPreSignedAddress|String|http://xxxx.oss-cn-shanghai.aliyuncs.com/driver/a534d3b81\*\*\*\*\*\*\*8fe7da0/DRIVER\_VERSION\_CONTENT/df9b9f441\*\*\*\*\*\*\*\*\*4c90d0c21d14/2.0.0/1581586102750/driver\_code.zip?Expires\\u003d1581586402\\u0026OSSAccessKeyId\\u003daS4MT0IYrP\*\*\*\*\*\*\\u0026Signature\\u003dIUUjZ881H3rUoCOwjMXPmGbw\*\*\*\*\*\*|The pre-signed URL of the OSS object. For more information, see [OSS documentation](~~32016~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|91E2BFA2-ECD7-4E11-B36B-66BCC4773922|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=CreateEdgeOssPreSignedAddress
&Type=DRIVER_VERSION_CONTENT
&ResourceId=df9b9f441*********4c90d0c21d14
&FileName=driver_code.zip
&ResourceVersion=2.0.0
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

