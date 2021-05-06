---
keyword: [Internet of Things, IoT Platform, IoT, SDK for PHP, API call]
---

# Use IoT Platform SDK for PHP

IoT Platform provides developers with an SDK for PHP. This article describes how to install and configure IoT Platform SDK for PHP. This article also describes how to use the SDK to call the API operations of IoT Platform.

## Install the SDK

IoT Platform SDK for PHP is part of [Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php). If you have installed Alibaba Cloud SDK for PHP, you do not need to install IoT Platform SDK for PHP.

1.  Install PHP.

    PHP 5.5.0 and later are supported. Download a PHP installation package from the [official PHP website](http://www.php.net/) and install PHP.

2.  Install Composer.

    Composer is used to manage IoT Platform SDK for PHP. Therefore, you must install Composer in your system.

    -   If you use Windows, you can download the [Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe) program from the [getcomposer.org](https://getcomposer.org/) website and install Composer.
    -   You can also run the following curl command to install Composer:

        ```
        curl -sS https://getcomposer.org/installer | php
        ```

    **Note:** If the installation fails due to network issues, you can use the [full image of Alibaba Cloud Composer](https://developer.aliyun.com/composer).

3.  Add the following dependency to install IoT Platform SDK for PHP:

    ```
    composer require alibabacloud/iot
    ```

    For more information, see [IoT Platform SDK for PHP](https://github.com/aliyun/openapi-sdk-php/tree/master/src/Iot) and [Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php).


## Initialize the SDK

The following example shows how to initialize the SDK if your IoT Platform service is deployed in the China \(Shanghai\) region:

```
<?php
include_once 'aliyun-php-sdk-core/Config.php';
use \Iot\Request\V20180120 as Iot;
// Set your AccessKey ID, AccessKey secret, and ProductKey.
$accessKeyId = "";
$accessSecret = "";
$iClientProfile = DefaultProfile::getProfile("cn-shanghai", $accessKeyId, $accessSecret);
$client = new DefaultAcsClient($iClientProfile);
```

|Parameter|Description|
|---------|-----------|
|$accessKeyId|The AccessKey ID of your Alibaba Cloud account. You can go to the [User Management console](https://ak-console.aliyun.com) to create or view your AccessKey ID. |
|$accessSecret|The AccessKey secret of your Alibaba Cloud account.|
|$iClientProfile|The object that is used to store the SDK initialization information. `cn-shanghai` indicates the region ID of your IoT Platform service. You can view the region in the upper-left corner of the [IoT Platform console](http://iot.console.aliyun.com/).

For more information about region IDs, see [Regions and zones](). |

## Initiate a request

The SDK encapsulates a class for each API operation. The class name is in the `${Operation name}+"Request"` format. For information about the API operations of IoT Platform, see [List of operations by function](/intl.en-US/Developer Guide (Cloud)/API reference/List of operations by function.md).

The following example shows how to call the Pub operation to publish a message to a topic.

For information about how to set request parameters in the `request`, see the corresponding API documentation. In this example, see [Pub](/intl.en-US/Developer Guide (Cloud)/API reference/Communications/Pub.md).

```
$request = new Iot\PubRequest(); 
$request->setProductKey("productKey");
$request->setMessageContent("aGVsbG93b3JsZA="); //hello world Base64 String.
$request->setTopicFullName("/productKey/deviceName/get"); // The full name of the topic to which the message is sent.
$response = $client->getAcsResponse($request);
print_r($response);
```

## Appendix: Sample code

Download the [SDK demo](https://github.com/aliyun/iotx-api-demo). The demo includes the sample code for Java, Python, PHP, .NET, and Go.

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com) to simplify API usage. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate the sample code of API operations for different SDKs. On the right side of the page, you can view the sample code of an SDK on the **Example Code** tab. On the **Debugging Result** tab, you can view the actual request URL and response in the JSON format.

