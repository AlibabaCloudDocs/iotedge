# SearchThings

使用该接口，按指定过滤条件搜索设备。

## 请求语法

```
POST /2020-04-30/things/search HTTP/1.1
Cookie: Cookie

Payload
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|
|Payload|JSON|是|JSON格式字符串。当前仅支持按标签搜索设备，可设置多个标签，搜索同时满足所有标签的设备。 格式请见表格下方请求Payload格式。 |

请求Payload格式如下所示。

```
{
  "Tags": {
    "Key1": "value1",
    "Key2": "value2"
    ...
  }
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
|StatusCode|Number|HTTP状态码。返回200表示成功，返回其它状态码表示失败。错误码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|Payload|JSON|搜索到的设备信息。|

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
        "Tags": [{"Key1": "Value1"}],
        "Status": "Inactivated|Failed|Online|Offline",
        "Connected": true|false,
        "ConnectTime": "string"
      }]
    }
  }
```

## 完整示例

```
$ curl -i -b token.cookie -d '{"Tags":{"Name":"LightSensor"}}' -k -X POST https://127.0.0.1:9999/2020-04-30/things/search

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Wed, 22 Apr 2020 15:18:16 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive

{"Data":{"Things":[{"DriverName":"LightSensor","Status":"Online","NickName":"","DriverId":"e0bb1b48964e4519b4a52f9b****1dd3","ProductKey":"a1t****n42K","Connected":true,"ConnectTime":"1587526047107","DeviceName":"test","ProductName":"","Tags":{"Name":"LightSensor"}}]}}
```

