# SetThingProperties

使用该接口为指定的设备设置属性。

## 请求语法

```
POST /2020-04-30/things/ProductKey/DeviceName/properties HTTP/1.1
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
|Payload|JSON|是|设置设备属性。格式请见表格下方请求Payload格式。|

请求Payload格式如下所示。

```
{
  "Properties": {
    "Identifier1": value1,
    "Identifier2": value2,
    "Identifier3": value3,
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
|StatusCode|Number|HTTP状态码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|Payload|JSON|底层属性设置接口返回的内容。|

返回Payload格式如下所示。

```
{ 
  "Data": {
    "Data": string|boolean|number|array|object, // A optional data that returned from the underlying set
    "Timestamp": 1568262117344
  }
}
```

## 完整示例

```
curl -i -b token.cookie -d '{"Properties":{"LightSwitch":0}}' -k -X POST https://127.0.0.1:9999/2020-04-30/things/a1W****CGHU/N0hB9tiVWWZF****KHgs/properties

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Wed, 22 Apr 2020 17:06:07 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive

{"Data":{"Data":[],"Timestamp":1587575167259}}
```

