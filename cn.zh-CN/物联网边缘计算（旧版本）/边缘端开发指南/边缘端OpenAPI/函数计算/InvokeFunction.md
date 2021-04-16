# InvokeFunction

使用该接口调用指定的函数。

## 请求语法

```
POST /2020-04-30/functions/Function/invocations HTTP/1.1
Cookie: Cookie

Payload
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|Function|String|是|需要调用的函数信息。有如下两种ARN形式： -   完整的ARN形式：格式为`acs:fc:<yourRegion\>:<yourAccountId\>:service:<yourServiceName\>:function:<yourFunctionName\>`。
-   部分ARN形式：格式为`service:<yourServiceName\>:function:<yourFunctionName\>`。

**说明：** ARN的格式必须符合如下正则表达式模式。

`(^acs:fc:([a-z]{2}-[a-z]+(-\d)?)?:(\d{16})?:)?service:([a-zA-Z][\w-]{0,127}):function:([a-zA-Z][\w-]{0,127})$` |
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|
|Payload|JSON|是|Payload的内容将原封不动地传给函数。|

## 返回语法

```
HTTP/1.1 StatusCode
X-Fc-Error-Type: ErrorType

Payload
```

## 返回参数

|参数名称|类型|描述|
|----|--|--|
|StatusCode|Number|HTTP状态码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|ErrorType|String|在函数执行发生错误时出现的参数。有如下两种值： -   Handled：表示函数上报的错误。
-   Unhandled：表示由函数计算检测并上报的错误，包括函数处理超时或内存不足等错误。 |
|Payload|JSON|函数返回的内容，或者返回如下Payload格式所示的错误信息。|

返回Payload格式如下所示。

```
{
    "Message": "string",
    "StackTrace": []
}
```

## 完整示例

```
$ curl -i -b token.cookie -k -X POST https://127.0.0.1:9999/2020-04-30/functions/service:helloworld:function:helloworld/invocations

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Tue, 21 Apr 2020 14:37:38 GMT
Content-Type: text/plain; charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive

Hello World
```

