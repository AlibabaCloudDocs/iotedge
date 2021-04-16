# EnableScene

使用该接口启用指定的场景联动规则。

## 请求语法

```
POST /2020-04-30/scenes/Scene/enable HTTP/1.1
Cookie: Cookie
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|Scene|String|是|指定场景联动规则的ID。调用[ListScenes](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/场景联动/ListScenes.md)接口获取场景联动规则ID。|
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|

## 返回语法

```
HTTP/1.1 StatusCode
Content-Type: application/json
```

## 返回参数

|参数名称|类型|描述|
|----|--|--|
|StatusCode|Number|HTTP状态码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|

## 完整示例

```
$ curl -i -b token.cookie -k -X POST https://127.0.0.1:9999/2020-04-30/scenes/d14122632aaf4d1d8e325963****9528/enable

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Thu, 16 Apr 2020 01:51:27 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
```

