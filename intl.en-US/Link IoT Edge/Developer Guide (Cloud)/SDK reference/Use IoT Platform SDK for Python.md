---
keyword: [Internet of Things, IoT, IoT Platform, device, SDK for Python, API]
---

# Use IoT Platform SDK for Python

IoT Platform provides developers with an SDK for Python. This article describes how to install and configure IoT Platform SDK for Python. This article also describes how to use the SDK to call the API operations of IoT Platform.

## Install the SDK

1.  Install Python.

    Download a Python installation package from the [official Python website](https://www.python.org/downloads/) and install Python. Python 2.7.x and 3.x are supported.

2.  Install pip that is used to manage Python packages.If you have installed pip, skip this step.

    Download a pip installation package from the [official pip website](https://pip.pypa.io/en/stable/installing/) and install pip.

3.  Install IoT Platform SDK for Python.

    Run the following commands as an administrator to install IoT Platform SDK for Python. For more information, see [IoT Platform SDK for Python](https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-iot).

    ```
    sudo pip install aliyun-python-sdk-core
    sudo pip install aliyun-python-sdk-iot
    ```

4.  Import the files that are related to IoT Platform SDK for Python to a Python file.

    ```
    from aliyunsdkcore import client
    from aliyunsdkiot.request.v20180120 import RegisterDeviceRequest
    from aliyunsdkiot.request.v20180120 import PubRequest
    ...
    ```


## Initialize the SDK

The following example shows how to initialize the SDK if your IoT Platform service is deployed in the China \(Shanghai\) region:

```
accessKeyId = '<your accessKey>'
accessKeySecret = '<your accessSecret>'
clt = client.AcsClient(accessKeyId, accessKeySecret, 'cn-shanghai')
```

|Parameter|Description|
|---------|-----------|
|accessKeyId|The AccessKey ID of your Alibaba Cloud account. You can go to the [User Management console](https://ak-console.aliyun.com) to create or view your AccessKey ID. |
|accessKeySecret|The AccessKey secret of you Alibaba Cloud account.|
|clt|The initialized SDK client. `cn-shanghai` indicates the region ID of your IoT Platform service. You can view the region in the upper-left corner of the [IoT Platform console](http://iot.console.aliyun.com/).

For more information about region IDs, see [Regions and zones](). |

## Initiate a request

The SDK encapsulates a class for each API operation. The class name is in the `${Operation name}+"Request"` format. For information about the API operations of IoT Platform, see [List of operations by function](/intl.en-US/Developer Guide (Cloud)/API reference/List of operations by function.md).

The following example shows how to call the Pub operation to publish a message to a topic.

For information about how to set request parameters in the `request`, see the corresponding API documentation. In this example, see [Pub](/intl.en-US/Developer Guide (Cloud)/API reference/Communications/Pub.md).

```
request = PubRequest.PubRequest()
request.set_accept_format('json')  # The format in which the response is returned. By default, the XML format is used. In this example, the JSON format is used. 
request.set_ProductKey('productKey')
request.set_TopicFullName('/productKey/deviceName/get')  # The full name of the topic to which the message is sent.
request.set_MessageContent('aGVsbG8gd29ybGQ=')  #hello world Base64 String
request.set_Qos(0)
result = clt.do_action_with_exception(request)
print 'result : ' + result
```

## Appendix: Sample code

Download the [SDK demo](https://github.com/aliyun/iotx-api-demo). The demo includes the sample code for Java, Python, PHP, .NET, and Go.

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com) to simplify API usage. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate the sample code of API operations for different SDKs. On the right side of the page, you can view the sample code of an SDK on the **Example Code** tab. On the **Debugging Result** tab, you can view the actual request URL and response in the JSON format.

