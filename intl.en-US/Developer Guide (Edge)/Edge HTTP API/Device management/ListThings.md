# ListThings

Queries devices and their status.

## Request syntax

```
GET /2019-09-30/things HTTP/1.1
Cookie: Cookie
```

## Request parameters

|Parameter|Type|Required|Description|
|:--------|----|--------|:----------|
|Cookie|String|Yes|The authentication cookie generated when the [CreateAuthCookie](/intl.en-US/Developer Guide (Edge)/Edge HTTP API/Authentication/CreateAuthCookie.md) API operation is called.|

## Response syntax

```
HTTP/1.1 StatusCode
Content-Type: application/json

Payload
```

## Response Parameters

|Parameter|Type|Description|
|---------|----|-----------|
|StatusCode|Number|The status code. If the request is successful, 200 is returned. If the request fails, an error code is returned. For information about error codes, see [Status codes](/intl.en-US/Developer Guide (Edge)/Edge HTTP API/Status codes.md).|
|Payload|JSON|The device information that you have obtained.|

The format of the returned Payload is as follows:

```
{
    "Code": number,
    "Message": "success|reason for failure",
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

## Example

```
$ curl -i -b token.cookie -k https://127.0.0.1:9999/2019-09-30/things

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Thu, 31 Oct 2019 08:23:21 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive

{"Data":{"Things":[{"DriverName":"e0bb1b48964e4519b4a52f9b719e1***","ConnectTime":"1572510191943","DeviceName":"GjCb9LKXgcKXeluG****","DriverId":"","ProductKey":"","Connected":true,"ProductName":"","Tags":[],"Status":"Online"}]},"Code":200,"Message":"success"}
```

