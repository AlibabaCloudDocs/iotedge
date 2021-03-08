---
keyword: [物联网, IoT, 物联网平台, 设备, Java SDK, API]
---

# Java SDK使用说明

物联网平台的Java SDK让开发人员可以方便地使用Java程序操作物联网平台。开发者可以使用Maven依赖添加SDK，也可以下载安装包到本地直接安装。

## 安装SDK

1.  安装Java开发环境。

    您可以从[Java 官方网站](http://developers.sun.com/downloads/)下载，并按说明安装Java开发环境。

2.  安装IoT Java SDK。

    1.  访问[Apache Maven 官网](http://maven.apache.org/)下载Maven软件。

    2.  添加Maven项目依赖。

        -   最新版IoT Java SDK的Maven依赖坐标：

            ```
            <!-- https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-iot -->
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>aliyun-java-sdk-iot</artifactId>
                <version>7.8.0</version>
            </dependency>
            ```

        -   阿里云Java SDK公共包Maven依赖坐标：

            ```
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>aliyun-java-sdk-core</artifactId>
                <version>3.5.1</version>
            </dependency>
            ```


## 初始化SDK

```
String accessKey = "${accessKey}";
String accessSecret = "${accessSecret}";
IClientProfile profile = DefaultProfile.getProfile("${RegionId}", accessKey, accessSecret);
DefaultAcsClient client = new DefaultAcsClient(profile); //初始化SDK客户端。
```

|参数|说明|
|--|--|
|accessKey|您账号的AccessKey ID。您可在[阿里云官网控制台AccessKey管理](https://ak-console.aliyun.com)中创建或查看您的AccessKey。 |
|accessSecret|您账号的AccessKey Secret。|
|profile|profile对象用于存放SDK初始化信息，其中`${RegionId}`是您的物联网平台服务的地域代码。您可在[物联网平台控制台](http://iot.console.aliyun.com/)左上方，查看当前服务所在地域。

地域代码的表达方法，请参见[地域和可用区]()。 |

以调用华东2（上海）地域的API为例，初始化代码如下。

```
String accessKey = "${accessKey}";
String accessSecret = "${accessSecret}";
IClientProfile profile = DefaultProfile.getProfile("cn-shanghai", accessKey, accessSecret);
DefaultAcsClient client = new DefaultAcsClient(profile); 
```

## 发起调用

物联网平台云端SDK为每个API封装了一个类，命名为`${API名称}+"Request"`，用于API的调用请求。物联网平台云端API，请参见[API列表](/cn.zh-CN/云端开发指南/云端API参考/API列表.md)。

本文以调用Pub接口发布消息到Topic为例。

有关如何设置`request`中请求参数，请参见对应API文档。以下示例，请参见[Pub](/cn.zh-CN/云端开发指南/云端API参考/消息通信/Pub.md)。

**说明：** 以下代码中iotInstanceId为实例ID，企业版实例填写实例ID，公共实例要删除代码`request.setIotInstanceId("iotInstanceId");`。

关于如何购买企业版实例，并获取实例ID，请参见[实例管理](/cn.zh-CN/.md)。

```
PubRequest request = new PubRequest(); 
request.setIotInstanceId("${iotInstanceId}"); 
request.setProductKey("${productKey}"); 
request.setMessageContent(Base64.encodeBase64String("hello world".getBytes())); 
request.setTopicFullName("/${productKey}/${deviceName}/user/get"); 
request.setQos(0); //目前支持QoS0和QoS1。 
try 
{ 
   PubResponse response = client.getAcsResponse(request); 
   System.out.println(response.getSuccess()); 
   System.out.println(response.getErrorMessage());
} 
catch (ServerException e) 
{
   e.printStackTrace();
}
 catch (ClientException e)
{
   e.printStackTrace();
}
```

## 附录

阿里云OpenAPI开发者门户提供[API在线调试工具](https://next.api.aliyun.com/api/Iot)。在**API调试**页面，您可以快速检索和体验调用API。系统会根据您输入的参数同步生成各语言SDK的Demo代码。各语言SDK Demo显示在页面右侧**SDK示例**页签下供您参考。在**调用结果**页签下，查看API调用的真实请求URL和JSON格式的返回结果。

