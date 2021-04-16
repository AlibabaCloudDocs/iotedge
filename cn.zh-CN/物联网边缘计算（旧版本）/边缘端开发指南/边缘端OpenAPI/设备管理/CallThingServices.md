# CallThingServices

使用该接口进行设备的服务调用。

## 请求语法

```
POST /2020-04-30/things/ProductKey/DeviceName/services HTTP/1.1
Cookie: Cookie

Payload
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|ProductKey|String|是|设备所属产品的唯一标识符。可从物联网平台控制台获取。|
|DeviceName|String|是|设备的名称。可从物联网平台控制台获取。|
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|
|Payload|JSON|是|被调用服务的名称和参数。必须与在物联网平台控制台，为设备所属产品自定义产品功能时，设置的服务名称和参数保持一致。格式请见表格下方请求Payload格式。|

请求Payload格式如下所示。

```
{
  "Services": [
    {
      "Name": "string",
      "Args": args // Optional arguments for the service.
    }
  ]
}
```

## 返回语法

```
HTTP/1.1 StatusCode
Content-Type: application/json

Payload
```

## 返回参数

|参数名称|类型|描述|
|----|--|--|
|StatusCode|Number|接口返回码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|Payload|JSON|调用服务的返回信息。|

返回Payload格式如下所示。

```
{
  "Data": {
    "Services": [
      {
        "Name": "string",
        "Returns": {  
          "Code": "string", // Error code that returned from the underlying call to the thing service.
          "Message": "string", // Error message that returned from the underlying call services call.
          "Data": string|boolean|number|array|object, // An optional data that returned from the underlying call services call.
        }
      }
    ],
      "Timestamp": 1568262117344
  }
}
```

## 完整示例

```
$ curl -i -b token.cookie -d '{"Services":[{"Name":"setColor","Args": {"color":"red"}}]}' -k -X POST https://127.0.0.1:9999/2019-09-30/things/a1WabAEC***/N0hB9tiVWWZFMpALK***/services

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Thu, 31 Oct 2019 11:17:47 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive

{"Data":{"Services":[{"Name":"setColor","Returns":{"Message":"success","Data":[]}}],"Timestamp":1572520667899},"Code":200,"Message":"success"}
```

