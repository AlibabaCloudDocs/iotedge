# Make API requests

This article describes the structure of IoT Platform API requests and provides a sample request.

## Request structure

To send an IoT Platform API request, you must send an HTTP or HTTPS request to the IoT Platform endpoint.

A request uses the following syntax:

```
http://Endpoint/?Action=xx&Parameters
```

|Parameter|Description|
|:--------|:----------|
|Endpoint|The endpoint of the IoT Platform API. Set the value to `iot. ${RegionId}.aliyuncs.com`. Replace $\{RegionId\} with the ID of the region where you purchased the IoT Platform service. For more information about the IDs of Alibaba Cloud regions, see [Regions and zones](). Examples:

-   China \(Shanghai\): `iot.cn-shanghai.aliyuncs.com`
-   Singapore: `iot.ap-southeast-1.aliyuncs.com`
-   US \(Silicon Valley\): `iot.us-west-1.aliyuncs.com`
-   Japan \(Tokyo\): `iot.ap-northeast-1.aliyuncs.com`
-   Germany \(Frankfurt\): `iot.eu-central-1.aliyuncs.com` |
|Action|The name of the operation being performed. For example, to publish a message to a specified topic, you must set the Action parameter to Pub.|
|Parameters|The request parameters for the operation. Separate multiple parameters with ampersands \(&\). Request parameters include both [common parameters](/intl.en-US/Developer Guide (Cloud)/API reference/Common parameters.md) and operation-specific parameters. Common parameters include information such as the API version number and authentication information. |

The following code provides an example on how to call the Pub operation to publish a message to a topic:

**Note:** In this example, IoT Platform is activated in the China \(Shanghai\) region. The code has been formatted to ease reading.

```
https://iot.cn-shanghai.aliyuncs.com/?Action=Pub
&Format=XML
&Version=2017-04-20
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dgI%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=...
&Timestamp=2017-07-19T12:00:00Z
&RegionId=cn-shanghai
...
```

```
https://POP gateway domain name/data/api.json/?Action=Pub
&Format=XML
&Version=2017-04-20
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dgI%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&Timestamp=2017-07-19T12:00:00Z
...
```

## Debugging

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com) to simplify API usage. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate the sample code of API operations for different SDKs. On the right side of the page, you can view the sample code of an SDK on the **Example Code** tab. On the **Debugging Result** tab, you can view the actual request URL and response in the JSON format.

![IoT Platform API](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3643929951/p40697.png)

## Authorization

To ensure the security of your Alibaba Cloud account, we recommend that you call API operations as a RAM user. Before you call an API operation as a RAM user, you must create and attach specific authorization policies to the RAM user to allow access to the API operation.

For more information, see [API permissions](/intl.en-US/User Accounts/RAM authorization/Resource Access Management (RAM)/API permissions.md).

