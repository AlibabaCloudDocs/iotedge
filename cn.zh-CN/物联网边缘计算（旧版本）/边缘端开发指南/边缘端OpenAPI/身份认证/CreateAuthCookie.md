# CreateAuthCookie

使用该接口创建一个新的认证Cookie。

## 请求语法

```
POST /2020-04-30/auth/cookies
Authorization: Authorization
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|Authorization|String|是|支持Basic认证。格式为 `Basic base64(username:password)`。 例如`Basic Y2h5aW5n********NTY=`。

**说明：**

-   `username`为登录边缘网关控制台的用户名。
-   `password`为登录边缘网关控制台的密码。

详情请参见[登录边缘网关控制台](/cn.zh-CN/物联网边缘计算（旧版本）/用户指南/边缘网关控制台/登录边缘网关控制台.md)内容。 |

## 返回语法

```
HTTP/1.1 StatusCode
Set-Cookie: Cookie
Content-Type: application/json
```

## 返回参数

|参数名称|类型|描述|
|----|--|--|
|StatusCode|Number|HTTP状态码。返回201表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|Cookie|String|授权的认证Cookie，用于进一步的API调用。|

## 完整示例

```
curl -i -c token.cookie -u admin:admin1234 -k -X POST https://127.0.0.1:9999/2020-04-30/auth/cookies

HTTP/1.1 201 Created
Server: openresty/1.13.6.2
Date: Wed, 15 Apr 2020 11:03:05 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: token=e82c2e9b7fe55a42143d89d1d635cd90a8ecef772a9520e3547028ad6a******; Max-Age=3600; Path=/
```

