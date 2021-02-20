# PHP SDK

You can use the PHP SDK to manage IoT Platform.

## Install the IoT PHP SDK

1.  Install the PHP development environment.

    Go to the [PHP website](http://www.php.net/) to download the PHP installation package and complete the installation.

2.  Download and then extract the IoT PHP SDK package.

    Click [IoT PHP SDK Download Address](https://github.com/aliyun/aliyun-openapi-php-sdk/tree/master/aliyun-php-sdk-iot) to download the PHP SDK package, and then extract the package to the specified directory. The PHP SDK is a software development kit that does not require installation.


## Initialize the SDK

```
<? php
include_once 'aliyun-php-sdk-core/Config.php';
use \Iot\Request\V20180120 as Iot;
//Set your AccessKeyId, AccessSecret, and ProductKey.
$accessKeyId = "";
$accessSecret = "";
$iClientProfile = DefaultProfile::getProfile("cn-shanghai", $accessKeyId, $accessSecret);
$client = new DefaultAcsClient($iClientProfile);
```

accessKeyId is the AccessKeyId of your account.accessSecret is the AccessKeySecret for the AccessKeyId. You can go to [AccessKey](https://ak-console.aliyun.com) page in the console to create or view your AccessKey.

## Initiate a call

The following example shows how to call the Pub operation to publish data to a device.

```
$request = new Iot\PubRequest();
$request->setProductKey("productKey");
$request->setMessageContent("aGVsbG93b3JsZA="); //hello world Base64 String.
$ Request-> fig ("/product key/ergonomic ename/get "); // Full name of the topic that the message is sent to.
$response = $client->getAcsResponse($request);
print_r($response);
```

