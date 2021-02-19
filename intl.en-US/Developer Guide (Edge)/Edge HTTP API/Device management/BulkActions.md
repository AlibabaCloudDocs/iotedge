# BulkActions

Manage devices in batches.

## Request syntax

```
POST /2019-09-30/things/bulk HTTP/1.1
Cookie: Cookie

Payload
```

## Request Parameters

|Parameter|Type|Required|Description|
|:--------|----|--------|:----------|
|Cookie|String|Yes|The authentication cookie generated when the [CreateAuthCookie](/intl.en-US/Developer Guide (Edge)/Edge HTTP API/Authentication/CreateAuthCookie.md) API operation is called.|
|Payload|JSON|Yes|The JSON object that contains the actions \(BulkAction\), the target devices \(Things\), and related parameters. For more information, see the Payload format.|

The format of the request Payload is as follows:

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

|Parameter|Type|Required|Description|
|:--------|----|--------|:----------|
|BulkAction|String|Yes|The action that you want to perform. Valid values: -   SetProperites: sets device properties in batches.
-   GetProperites: obtains device properties in batches.
-   CallServices: calls device services in batches.
-   Watch: obtains a specified set of events from the device. |
|Things|Array|Yes|The JSON array that contains the object and operation parameters. For more information about the format, see the Things parameter defined in the [GetProperties](#section_6az_7kb_sdh), [SetProperties](#section_7cn_fpt_lz4), [CallServices](#section_hu0_9hk_9n8), and [Watch](#section_gu8_7kh_ogh) sections.|

## Response syntax

```
HTTP/1.1 StatusCode
Content-Type: ContentType

Payload
```

## Response Parameters

|Parameter|Type|Description|
|:--------|----|:----------|
|StatusCode|Number|The HTTP status code. If the request is successful, 200 is returned. If the request fails, other status codes are returned. For information, see [Status codes](/intl.en-US/Developer Guide (Edge)/Edge HTTP API/Status codes.md).|
|ContentType|String|The data type of the returned message \(Payload\). The data type depends on the specified action \(BulkAction\).|
|Payload|JSON|The response of the batch operation.|

```
{
  "Code": number,
  "Message": "success|reason for failure"
  "Data": {}
}
```

|Parameter|Type|Description|
|:--------|----|:----------|
|Code|Number|The status code of the operation. If the request is successful, 200 is returned. If the request fails, other status codes are returned. For information, see [Status codes](/intl.en-US/Developer Guide (Edge)/Edge HTTP API/Status codes.md).|
|Message|String|If the request is successful, `success` is returned. If the call fails, the reason for the failure is returned.|
|Data|Object|The returned result of a batch operation. For more information about the format, see the Data parameter defined in the [GetProperties](#section_6az_7kb_sdh), [SetProperties](#section_7cn_fpt_lz4), [CallServices](#section_hu0_9hk_9n8), and [Watch](#section_gu8_7kh_ogh) sections.|

## GetProperties

-   The format of the request Payload

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

-   The format of the returned Payload

    Content-Type: application/json

    ```
    {
      "Code": number,
      "Message": "success|reason for failure",
      "Data": {
        "Results": [
          {
            "ProductKey": "string",
            "DeviceName": "string",
            "Returns": {
              "Message": "success|reason for failure",
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

-   Example

    ```
    $ curl -i -b token.cookie -d '{"BulkAction":"GetProperties","Things":[{"ProductKey":"a1WabAEC***","DeviceName":"N0hB9tiVWWZFMpALK***","Identifiers":["LightSwitch"]}]}' -k -X POST https://127.0.0.1:9999//2019-09-30/things/bulk
    
    HTTP/1.1 200 OK
    Server: openresty/1.13.6.2
    Date: Thu, 31 Oct 2019 11:30:40 GMT
    Content-Type: application/json; charset=utf-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    
    {"Data":{"Results":[{"Returns":{"Message":"success","Data":{"LightSwitch":1}},"DeviceName":"N0hB9tiVWWZFMpALK***","ProductKey":"a1WabAEC***"}],"Timestamp":1572521440288},"Code":200,"Message":"success"}
    ```


## SetProperties

-   The format of the request Payload

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
            "Identifier3": value3
        ...
          }
        }
      ]
    }
    ```

-   The format of the returned Payload

    Content-Type: application/json

    ```
    {
      "Code": number,
      "Message": "success|reason for failure",
      "Data": {
        "Results": [
          {
            "ProductKey": "string",
            "DeviceName": "string",
            "Returns": {
              "Message": "success|reason for failure",
              "Data": string|boolean|number|array|object // An optional data that returned from the underlying set properties call.
            },
          }
        ],
        "Timestamp": 1568262117344
      }
    }
    ```

-   Example

    ```
    $ curl -i -b token.cookie -d '{"BulkAction":"SetProperties","Things":[{"ProductKey":"a1WabAEC***","DeviceName":"N0hB9tiVWWZFMpALK***","Properties":{"LightSwitch":1}}]}' -k -X POST https://127.0.0.1:9999//2019-09-30/things/bulk
    
    HTTP/1.1 200 OK
    Server: openresty/1.13.6.2
    Date: Thu, 31 Oct 2019 11:46:53 GMT
    Content-Type: application/json; charset=utf-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    
    {"Data":{"Results":[{"Returns":{"Message":"success","Data":[]},"DeviceName":"N0hB9tiVWWZFMpALK***","ProductKey":"a1WabAEC***"}],"Timestamp":1572522413633},"Code":200,"Message":"success"}
    ```


## CallServices

-   The format of the request Payload

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

-   The format of the returned Payload

    Content-Type: application/json

    ```
    {
      "Code": number,
      "Message": "success|reason for failure",
      "Data": {
        "Results": [
          {
            "ProductKey": "string",
            "DeviceName": "string",
            "Services": [
              {
                "Name": "string",
                "Returns": {
                  "Message": "success|reason for failure",
                  "Data": string|boolean|number|array|object // An optional data that returned from the underlying call services call.
                }
              }
            ],
          }
        ],
        "Timestamp": 1568262117344
      }
    }
    ```

-   Example

    ```
    $ curl -i -b token.cookie -d '{"BulkAction":"CallServices","Things":[{"ProductKey":"a1WabAEC***","DeviceName":"N0hB9tiVWWZFMpALK***","Services":[{"Name":"setColor","Args":{"color":"red"}}]}]}' -k -X POST https://127.0.0.1:9999//2019-09-30/things/bulk
    
    HTTP/1.1 200 OK
    Server: openresty/1.13.6.2
    Date: Thu, 31 Oct 2019 11:52:13 GMT
    Content-Type: application/json; charset=utf-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    
    {"Data":{"Results":[{"Services":[{"Name":"setColor","Returns":{"Message":"success","Data":[]}}],"DeviceName":"N0hB9tiVWWZFMpALK***","ProductKey":"a1WabAEC***"}],"Timestamp":1572522733310},"Code":200,"Message":"success"}
    ```


## Watch

-   The format of the request Payload

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

-   The format of the returned Payload

    Content-Type: text/plain

    -   Regular messages

        ```
        {
          "Code": number,
          "Message": "success|reason for failure",
          "Data": {
            "ProductKey": "string",
            "DeviceName": "string",
            "Event": "string",
            "Args": {}, // Optional arguments along with the event.
            "Timestamp": 1568010749340 
          }
        }
        ```

    -   Heartbeat messages

        ```
        {
          "Code": 200,
          "Message": "heartbeat",
          "Data": {
            "Timestamp": 1568010749340 
          }
        }
        ```

-   Example

    ```
    $ curl -b token.cookie -d '{"BulkAction":"Watch","Things":[]}' -k -X POST https://127.0.0.1:9999//2019-09-30/things/bulk
    
    {"Data":{"Timestamp":1572510704112,"Event":"propertiesChanged","ProductKey":"a1t9b6Nn***","Args":{"MeasuredIlluminance":{"time":1572510704110,"value":400}},"DeviceName":"GjCb9LKXgcKXeluGJ***"},"Code":200,"Message":"success"}
    {"Data":{"Timestamp":1572510706116,"Event":"propertiesChanged","ProductKey":"a1t9b6Nn***","Args":{"MeasuredIlluminance":{"time":1572510706114,"value":300}},"DeviceName":"GjCb9LKXgcKXeluGJ***"},"Code":200,"Message":"success"}
    {"Data":{"Timestamp":1572510706117},"Code":200,"Message":"heartbeat"}
    {"Data":{"Timestamp":1572510708119,"Event":"propertiesChanged","ProductKey":"a1t9b6Nn***","Args":{"MeasuredIlluminance":{"time":1572510708118,"value":200}},"DeviceName":"GjCb9LKXgcKXeluGJ***"},"Code":200,"Message":"success"}
    ```


