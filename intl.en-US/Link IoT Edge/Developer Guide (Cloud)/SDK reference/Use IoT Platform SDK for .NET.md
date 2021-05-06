---
keyword: [Internet of Things, IoT, IoT Platform, device, SDK for .NET, API]
---

# Use IoT Platform SDK for .NET

IoT Platform provides developers with an SDK for .NET. This article describes how to install and configure IoT Platform SDK for .NET. This article also describes how to use the SDK to call the API operations of IoT Platform.

## Install the SDK

1.  Install a .NET development environment.

    IoT Platform SDK for .NET supports the following development environments:

    -   .NET Framework 4.0 and later
    -   .NET Standard 2.0 and later
    -   C\# 4.0 and later
    -   Visual Studio 2010 and later
2.  Install IoT Platform SDK for .NET by using the NuGet package manager.

    In this example, Visual Studio is used.

    1.  In the Solution Explorer pane of Visual Studio, right-click your project and select **Manage NuGet Packages**.

    2.  In the NuGet Package Manager pane, click the **Browse** tab.

    3.  On the Browse tab, enter aliyun-net-sdk in the search box and select the [aliyun-net-sdk-iot](https://www.nuget.org/packages/aliyun-net-sdk-iot) package that is provided by Alibaba Cloud.

    4.  Click **Install**.


## Initialize the SDK

**Note:** In this example, the China \(Shanghai\) region and the corresponding endpoint are used. You can replace `cn-shanghai` in the clientProfile object with the region ID of your IoT Platform service.

```
using Aliyun.Acs.Core;
using Aliyun.Acs.Core.Exceptions;
using Aliyun.Acs.Core.Profile;
IClientProfile clientProfile = DefaultProfile.GetProfile("cn-shanghai", "<your-access-key-id>", "<your-access-key-secret>");
DefaultAcsClient client = new DefaultAcsClient(clientProfile);
```

You can go to the [User Management console](https://ak-console.aliyun.com) to create or view your AccessKey pairs. Then, you can replace `<your-access-key-id>` and `<your-access-key-secret>` in the clientProfile object with your AccessKey ID and AccessKey secret.

## Initiate a request

The SDK encapsulates a class for each API operation. The class name is in the `${Operation name}+"Request"` format. For information about the API operations of IoT Platform, see [List of operations by function](/intl.en-US/Developer Guide (Cloud)/API reference/List of operations by function.md).

The following example shows how to call the Pub operation to publish a message to a topic.

For information about how to set request parameters in the `request`, see the corresponding API documentation. In this example, see [Pub](/intl.en-US/Developer Guide (Cloud)/API reference/Communications/Pub.md).

```
PubRequest request = new PubRequest();
request.ProductKey = "<productKey>";
request.TopicFullName = "/<productKey>/<deviceName>/get";
byte[] payload = Encoding.Default.GetBytes("Hello World.");
String payloadStr = Convert.ToBase64String(payload);
request.MessageContent = payloadStr;
request.Qos = 0;
try
{
   PubResponse response = client.GetAcsResponse(request);
   Console.WriteLine("publish message result: " + response.Success);
   Console.WriteLine(response.ErrorMessage);
}
catch (ServerException e)
{
   Console.WriteLine(e.ErrorCode);
   Console.WriteLine(e.ErrorMessage);
}
catch (ClientException e)
{
   Console.WriteLine(e.ErrorCode);
   Console.WriteLine(e.ErrorMessage);
}
```

## Appendix: Sample code

Download the [SDK demo](https://github.com/aliyun/iotx-api-demo). The demo includes the sample code for Java, Python, PHP, .NET, and Go.

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com) to simplify API usage. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate the sample code of API operations for different SDKs. On the right side of the page, you can view the sample code of an SDK on the **Example Code** tab. On the **Debugging Result** tab, you can view the actual request URL and response in the JSON format.

