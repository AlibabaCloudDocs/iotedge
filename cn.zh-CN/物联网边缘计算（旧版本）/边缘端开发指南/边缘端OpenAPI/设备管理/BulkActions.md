# BulkActions

使用该接口批量操作设备。

## 请求语法

```
POST /2020-04-30/things/bulk HTTP/1.1
Cookie: Cookie

Payload
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|
|Payload|JSON|是|JSON对象，包含批量操作的动作（BulkAction）、操作对象（Things）及其相关参数。格式详情，请参见表格下方Payload格式。|

请求Payload格式如下所示。

```
{
  "BulkAction": "string"
  "Things": [
    {
      "ProductKey": "string",
      "DeviceName": "string",
      ... // Parameters for BulkAction
    }
  ]
}
```

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|BulkAction|String|是|指定请求的批量操作。 必须是如下指定参数之一： -   SetProperites：表示批量设置设备属性。
-   GetProperites：表示批量获取设备属性。
-   CallServices：表示批量调用设备服务。
-   Watch：表示获取设备的某一组指定事件。 |
|Things|Array|是|JSON数组，包含操作对象及其对应的操作参数。格式详情，请参见本文下方[GetProperties](#section_6az_7kb_sdh)、[SetProperties](#section_7cn_fpt_lz4)、[CallServices](#section_hu0_9hk_9n8)、[Watch](#section_gu8_7kh_ogh)中请求Payload格式的Things参数。|

## 返回语法

```
HTTP/1.1 StatusCode
Content-Type: ContentType

Payload
```

## 返回参数

|参数名称|类型|描述|
|:---|--|:-|
|StatusCode|Number|HTTP状态码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|ContentType|String|返回消息（Payload）的类型。取决于批量操作的动作（BulkAction）。|
|Payload|JSON|批量操作的返回结果。|

返回Payload格式如下所示。

```
{
  "Data": {}
}
```

|参数名称|类型|描述|
|:---|--|:-|
|Data|Object|具体批量操作的返回结果。格式详情，请参见本文下方[GetProperties](#section_6az_7kb_sdh)、[SetProperties](#section_7cn_fpt_lz4)、[CallServices](#section_hu0_9hk_9n8)、[Watch](#section_gu8_7kh_ogh)中返回Payload格式的Data参数。|

## GetProperties

-   请求Payload格式

    ```
    {
      "BulkAction": "GetProperties",
      "Things": [
        {
          "ProductKey": "string",
          "DeviceName": "string",
          "Identifiers": [ // Property Identifiers
            "string",
            "string",
            "string",
            ...
          ]
        }
      ]
    }
    ```

-   返回Payload格式

    Content-Type：application/json

    ```
    {  
      "Data": {
        "Results": [
          {
            "ProductKey": "string",
            "DeviceName": "string",
            "Returns": {
              "Code": "string", // Error code
              "Message": "reason for failure", // Error message
              "Data": { // The properties returned from the underlying get properties call.
                "Identifier1": value1,
                "Identifier2": value2,
                "Identifier3": value3
                  ...
              }
            },
          }
        ],
        "Timestamp": 1568262117344
      }
    }
    ```

-   完整示例

    ```
    $ curl -i -b token.cookie -d '{"BulkAction":"GetProperties","Things":[{"ProductKey":"a1W****CGHU","DeviceName":"N0hB9tiVWWZF****KHgs","Identifiers":["LightSwitch"]}]}' -k -X POST https://127.0.0.1:9999/2020-04-30/things/bulk
    
    HTTP/1.1 200 OK
    Server: openresty/1.13.6.2
    Date: Wed, 22 Apr 2020 17:41:04 GMT
    Content-Type: application/json; charset=utf-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    
    {"Data":{"Results":[{"Returns":{"Data":{"LightSwitch":0}},"DeviceName":"N0hB9tiVWWZF****KHgs","ProductKey":"a1W****CGHU"}],"Timestamp":1587577264304}}
    ```


## SetProperties

-   请求Payload格式

    ```
    {
      "BulkAction": "SetProperties",
      "Things": [
        {
          "ProductKey": "string",
          "DeviceName": "string",
          "Properties": {
            "Identifier1": value1,
            "Identifier2": value2,
            "Identifier3": value3,
        ...
          }
        }
      ]
    }
    ```

-   返回Payload格式

    Content-Type：application/json

    ```
    {
      "Data": {
        "Results": [
          {
            "ProductKey": "string",
            "DeviceName": "string",
            "Returns": {
              "Code": "string", // Error code
              "Message": "reason for failure", // Error message
              "Data": string|boolean|number|array|object // A optional data that returned from the underlying set properties call.
            },
          }
        ],
        "Timestamp": 1568262117344
      }
    }
    ```

-   完整示例

    ```
    curl -i -b token.cookie -d '{"BulkAction":"SetProperties","Things":[{"ProductKey":"a1W****CGHU","DeviceName":"N0hB9tiVWWZF****KHgs","Properties":{"LightSwitch":1}}]}' -k -X POST https://127.0.0.1:9999/2020-04-30/things/bulk
    
    HTTP/1.1 200 OK
    Server: openresty/1.13.6.2
    Date: Wed, 22 Apr 2020 17:44:21 GMT
    Content-Type: application/json; charset=utf-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    
    {"Data":{"Results":[{"Returns":{"Data":[]},"DeviceName":"N0hB9tiVWWZF****KHgs","ProductKey":"a1W****CGHU"}],"Timestamp":1587577461238}}
    ```


## CallServices

-   请求Payload格式

    ```
    {
      "BulkAction": "CallServices",
      "Things": [
        {
          "ProductKey": "string",
          "DeviceName": "string",
          "Services": [
            {
              "Name": "string",
              "Args": args // Optional arguments for the service.
            }
          ]
        }
      ]
    }
    ```

-   返回Payload格式

    Content-Type：application/json

    ```
    { 
      "Data": {
        "Results": [
          {
            "ProductKey": "string",
            "DeviceName": "string",
            "Services": [
              {
                "Name": "string",
                "Returns": {
                  "Code": "string", // Error code
                  "Message": "reason for failure", // Error message
                  "Data": string|boolean|number|array|object // A optional data that returned from the underlying call services call.
                }
              }
            ],
          }
        ],
        "Timestamp": 1568262117344
      }
    }
    ```

-   完整示例

    ```
    curl -i -b token.cookie -d '{"BulkAction":"CallServices","Things":[{"ProductKey":"a1W****CGHU","DeviceName":"N0hB9tiVWWZF****KHgs","Services":[{"Name":"setColor","Args":{"color":"red"}}]}]}' -k -X POST https://127.0.0.1:9999//2020-04-30/things/bulk
    
    HTTP/1.1 200 OK
    Server: openresty/1.13.6.2
    Date: Wed, 22 Apr 2020 17:47:02 GMT
    Content-Type: application/json; charset=utf-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    
    {"Data":{"Results":[{"Services":[{"Name":"setColor","Returns":{"Data":[]}}],"DeviceName":"N0hB9tiVWWZF****KHgs","ProductKey":"a1W****CGHU"}],"Timestamp":1587577622555}}
    ```


## Watch

-   请求Payload格式

    ```
    {
      "BulkAction": "Watch",
      "Things": [
        {
          "ProductKey": "string",
          "DeviceName": "string",
          "Watches": "all|properties|events" // default is "all"
        }
      ]
    }
    ```

-   返回Payload格式

    Content-Type：text/plain

    -   常规消息

        ```
        {
          "Message": "success",
          "Data": {
            "ProductKey": "string",
            "DeviceName": "string",
            "Event": "string",
            "Args": {}, // Optional arguments along with the event.
            "Timestamp": 1568010749340 
          }
        }
        ```

    -   心跳消息

        ```
        {
          "Message": "heartbeat",
          "Data": {
            "Timestamp": 1568010749340 
          }
        }
        ```

-   完整示例

    ```
    $ curl -b token.cookie -d '{"BulkAction":"Watch","Things":[]}' -k -X POST https://127.0.0.1:9999//2020-04-30/things/bulk
    
    {"Message":"success","Data":{"Timestamp":1587577766731,"Event":"propertiesChanged","ProductKey":"a1t9b******","Args":{"MeasuredIlluminance":{"time":1587577766729,"value":200}},"DeviceName":"GjCb9LKXgcKXel******"}}
    {"Message":"heartbeat","Data":{"Timestamp":1587577767732}}
    {"Message":"success","Data":{"Timestamp":1587577768734,"Event":"propertiesChanged","ProductKey":"a1t9b******","Args":{"MeasuredIlluminance":{"time":1587577768733,"value":100}},"DeviceName":"GjCb9LKXgcKXel******"}}
    ```


