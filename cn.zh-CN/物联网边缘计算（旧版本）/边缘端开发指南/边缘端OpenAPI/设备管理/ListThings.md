# ListThings

使用该接口，列出所有设备及其状态。您也可以传入ProductKey来过滤指定产品下的设备，或者同时传入ProductKey和DeviceName返回某个具体设备。

## 请求语法

```
GET /2020-04-30/things?productkey=ProductKey&devicename=DeviceName HTTP/1.1
Cookie: Cookie
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|ProductKey|String|否|设备所属产品唯一标识符。|
|DeviceName|String|否|设备名。|
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|

## 返回语法

```
HTTP/1.1 StatusCode
Content-Type: application/json

Payload
```

## 返回参数

|参数名称|类型|描述|
|----|--|--|
|StatusCode|Number|接口状态码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|Payload|JSON|已获取的设备信息。|

返回Payload格式如下所示。

```
{   
    "Data": {
      "Things": [{
        "ProductName": "string",
        "ProductKey": "string",
        "DeviceName": "string",
        "DriverId": "string",
        "DriverName": "string",
        "Tags": [{"string": "string"}],
        "Status": "Inactivated|Failed|Online|Offline",
        "Connected": true|false,
        "ConnectTime": "string"
      }]
    }
  }
```

## 完整示例

```
$ curl -i -b token.cookie -k https://127.0.0.1:9999/2020-04-30/things

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Wed, 22 Apr 2020 15:18:16 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive

{"Data":{"Things":[{"DriverName":"LightSensor","Status":"Online","NickName":"","DriverId":"e0bb1b48964e4519b4a52f9b****1dd3","ProductKey":"a1t****n42K","Connected":true,"ConnectTime":"1587526047107","DeviceName":"GjCb9LKXgcKXel******","ProductName":"","Tags":[]}]}}
```

