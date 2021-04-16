# DeleteAuthCookie

使用该接口删除认证Cookie。

## 请求语法

```
DELETE /2020-04-30/auth/cookies/Token
Cookie: Cookie
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|Token|String|是|认证Cookie的Token。|
|Cookie|String|是|从[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)中获取的认证Cookie。|

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
$ curl -i -b token.cookie -k -X DELETE https://127.0.0.1:9999/2020-04-30/auth/cookies/e82c2e9b7fe55a42143d89d1d635cd90a8ecef772a9520e3547028ad6a******

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Wed, 15 Apr 2020 11:03:40 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
```

