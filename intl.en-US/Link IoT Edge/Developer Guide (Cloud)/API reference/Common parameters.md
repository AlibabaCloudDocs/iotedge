# Common parameters

This article describes the common request parameters and common response parameters that are used in IoT Platform API operations.

## Common request parameters

Common request parameters must be included in all IoT Platform API requests.

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Format|String|No|The format in which to return the response. Valid values: JSON and XML. Default value: XML.|
|Version|String|Yes|The version number of the API. The value must be in the `YYYY-MM-DD` format. The latest version is `2018-01-20`. Each API has multiple versions.|
|AccessKeyId|String|Yes|The AccessKey ID provided to you by Alibaba Cloud. To obtain the AccessKey ID, log on to the Alibaba Cloud Management Console, move the pointer over the user profile, and then click **AccessKey Management**. In the User Management console, you can view or create AccessKey pairs. |
|Signature|String|Yes|The signature string of the current request.|
|SignatureMethod|String|Yes|The encryption method of the signature string. Set the value to HMAC-SHA1.|
|Timestamp|String|Yes|The timestamp of the request. Specify the time in the ISO 8601 standard in the `YYYY-MM-DDThh:mm:ssZ` format. The time must be in UTC. For example, you can set the parameter to `2016-01-04T12:00:00Z`, which indicates January 4, 2016 20:00:00 UTC+8. |
|SignatureVersion|String|Yes|The version of the signature encryption algorithm. Set the value to 1.0.|
|SignatureNonce|String|Yes|A unique, random number used to prevent replay attacks. You must use different numbers for different requests.|
|RegionId|String|Yes|The region where your devices reside. The region you specify must match the region that is specified in the console. Example: cn-shanghai.|

Examples

```
https://iot.cn-shanghai.aliyuncs.com/
? Format=XML
&Version=2018-01-20
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dgI%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=...
&Timestamp=2018-05-20T12:00:00Z
&RegionId=cn-shanghai
```

## Common response parameters

API responses use the HTTP response format where a 2XX status code indicates a successful call and a 4XX or 5XX status code indicates a failed call. Responses can be returned in either the JSON or XML format. You can specify the response format in the request. The default response format is XML.

Every response returns a unique RequestId regardless of whether the call is successful.

-   Sample success responses

    -   XML format

        ```
        <? xml version="1.0" encoding="UTF-8"? > 
        <!--Root node of the response-->
        <Operation name+Response>
            <!--Return request tag-->
            <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
            <!--Response result data-->
        </Operation name+Response>
        ```

    -   JSON format

        ```
        {
            "RequestId": "4C467B38-3910-447D-87BC-AC049166F216"
            /* Response result data */
        }
        ```

-   Sample error responses

    If an error occurs when you call an API operation, no result is returned. You can use the error code to identify the cause.

    If an error occurs when you call an API operation, a 4XX or 5XX HTTP status code is returned. The response body contains the specific error code and error message. It also contains a globally unique request ID \(RequestId\). If you cannot confirm what error occurs, contact Alibaba Cloud customer service or submit a ticket. You must provide your request ID for assistance.

    -   XML format

        ```
        <? xml version="1.0" encoding="UTF-8"? >
        <Error>
           <RequestId>8906582E-6722-409A-A6C4-0E7863B733A5</RequestId>
           <Code>UnsupportedOperation</Code>
           <Message>The specified action is not supported. </Message>
        </Error>
        ```

    -   JSON format

        ```
        {
            "RequestId": "8906582E-6722-409A-A6C4-0E7863B733A5",
            "Code": "UnsupportedOperation",
            "Message": "The specified action is not supported."
        }
        ```


