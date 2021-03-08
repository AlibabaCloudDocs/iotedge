---
keyword: [物联网, 物联网平台, IoT, PHP SDK, 调用 API]
---

# PHP SDK使用说明

物联网平台提供PHP语言的云端SDK供开发人员使用。本文介绍云端PHP SDK的安装和配置，及使用PHP SDK调用云端API的示例。

## 安装PHP SDK

IoT PHP SDK是[Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php)的一部分。如果您已安装Alibaba Cloud SDK for PHP，则无需再安装IoT PHP SDK。

1.  安装PHP开发环境。

    需安装PHP 5.5.0或更高版本。访问[PHP官网](http://www.php.net/)下载PHP安装包，并完成安装。

2.  安装Composer。

    目前，通过Composer管理IoT PHP SDK，因此需在系统中安装Composer。

    -   Windows系统用户，请访问[getcomposer.org](https://getcomposer.org/)，下载、安装[Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe)。
    -   使用cURL命令安装Composer。

        ```
        curl -sS https://getcomposer.org/installer | php
        ```

    **说明：** 如果由于网络问题无法安装，可以使用[阿里云Composer全量镜像](https://developer.aliyun.com/composer)。

3.  添加以下依赖，安装IoT PHP SDK。

    ```
    composer require alibabacloud/iot
    ```

    PHP SDK详情和使用指导，请参见[openapi-sdk-php-iot](https://github.com/aliyun/openapi-sdk-php/tree/master/src/Iot)和[Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php)。


## 初始化SDK

以调用华东2（上海）地域的API为例，初始化代码如下。

```
<?php
include_once 'aliyun-php-sdk-core/Config.php';
use \Iot\Request\V20180120 as Iot;
//设置您的AccessKeyId/AccessSecret/ProductKey
$accessKeyId = "";
$accessSecret = "";
$iClientProfile = DefaultProfile::getProfile("cn-shanghai", $accessKeyId, $accessSecret);
$client = new DefaultAcsClient($iClientProfile);
```

|参数|说明|
|--|--|
|$accessKeyId|您账号的AccessKey ID。您可在[阿里云官网控制台AccessKey管理](https://ak-console.aliyun.com)中创建或查看您的AccessKey。 |
|$accessSecret|您账号的AccessKey Secret。|
|$iClientProfile|用于存放SDK初始化信息，其中`cn-shanghai`是您的物联网平台服务的地域代码。您可在[物联网平台控制台](http://iot.console.aliyun.com/)左上方，查看当前服务所在地域。

地域代码的表达方法，请参见[地域和可用区]()。 |

## 发起调用

物联网平台云端SDK为每个API封装了一个类，命名为`${API名称}+"Request"`，用于API的调用请求。物联网平台云端API，请参见[API列表](/cn.zh-CN/云端开发指南/云端API参考/API列表.md)。

本文以调用Pub接口发布消息到Topic为例。

有关如何设置`request`中请求参数，请参见对应API文档。以下示例，请参见[Pub](/cn.zh-CN/云端开发指南/云端API参考/消息通信/Pub.md)。

**说明：** 以下代码中iotInstanceId为实例ID，企业版实例填写实例ID，公共实例要删除代码`$request->setIotInstanceId("iotInstanceId");`。

关于如何购买企业版实例，请参见[实例管理](/cn.zh-CN/.md)。

```
$request = new Iot\PubRequest();
$request->setIotInstanceId("iotInstanceId"); 
$request->setProductKey("productKey");
$request->setMessageContent("aGVsbG93b3JsZA="); //hello world Base64 String.
$request->setTopicFullName("/productKey/deviceName/user/get"); //消息发送到的Topic全名.
$response = $client->getAcsResponse($request);
print_r($response);
```

## 附录：Demo

下载[物联网平台云端SDK Demo](https://github.com/aliyun/iotx-api-demo)。Demo中包含Java、Python、PHP、.NET和Go版本SDK示例。

阿里云OpenAPI开发者门户提供[API在线调试工具](https://next.api.aliyun.com/api/Iot)。在**API调试**页面，您可以快速检索和体验调用API。系统会根据您输入的参数同步生成各语言SDK的Demo代码。各语言SDK Demo显示在页面右侧**SDK示例**页签下供您参考。在**调用结果**页签下，查看API调用的真实请求URL和JSON格式的返回结果。

