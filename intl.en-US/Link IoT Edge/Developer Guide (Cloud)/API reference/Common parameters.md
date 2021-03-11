# Common parameters

This section lists the common request parameters and response parameters of the IoT Platform API.

## Common request parameters

Common request parameters are the request parameters required every time you call the API.

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Format|String|No|Format of the response data. JSON and XML are supported. The default value is XML.|
|Version|String|Yes|The API version number. The parameter value needs to be in the `YYYY-MM-DD` format. The latest version is `2018-01-20` . Each API operation may have multiple versions.|
|AccessKeyId|String|Yes|The access key ID issued by Alibaba Cloud for users to access services.|
|Signature|String|Yes|Signature string.|
|SignatureMethod|String|Yes|The signature method. Currently, HMAC-SHA1 is supported.|
|Timestamp|String|Yes|Required timestamp Date is in ISO8601 format, and must use UTC time. The parameter value needs to be in the `YYYY-MM-DDThh:mm:ssZ` format. For example, you can set the parameter to `2016-01-04T12:00:00Z`, which indicates January 4, 2016 20:00:00 Beijing Time \(UTC+8\). |
|SignatureVersion|String|Yes|The signature algorithm version. The current version is 1.0.|
|SignatureNonce|String|Yes|The unique random number. It is used to prevent replay attacks. You need to use different random numbers in different requests.|
|RegionId|String|Yes|The region where your devices are located. The region you specify must match the region specified in the console, for example, cn-shanghai.|

**Example**

```
https://iot.cn-shanghai.aliyuncs.com/
? Format=XML
&Version=2018-01-20
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1******
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=123***
&Timestamp=2018-05-20T12:00:00Z
&RegionId=cn-shanghai
```

## Common response parameters

The response parameters are displayed in specific formats. If HTTP status code 2xx is returned, the API operation call was successful. If HTTP status code 4xx or 5xx is returned, the API operation call has failed. The response data can be in either XML or JSON. You can specify the format of response data when sending your request. By default, response data is in the XML format.

Regardless of whether your API operation call is successful or not, the system returns RequestId as a unique identifier.

-   **Formats of data returned by a successful call**

    -   JSON format

        ```
        {
            "RequestId": "4C467B38-3910-447D-87BC-AC049166F216"
            /* Response data */
        }
        ```

    -   XML format

        ```
        <? xml version="1.0" encoding="UTF-8"? > 
        <!--Root node of the response data-->
        <API operation name+Response>
            <!--Request tag-->
            <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
            <!--Response data-->
        </API operation name+Response>
        ```

-   **Formats of data returned by a failed call**

    If any error occurs when you call an API operation, no data is returned. You can use the error code to locate the cause.

    If an error occurs, an HTTP status code 4xx or 5xx is returned. The returned message body contains the specific error code and error message. It also contains a globally unique request ID \(RequestID\). If you cannot confirm what error occurs, contact Alibaba Cloud customer service and provide your request ID for assistance.

    -   JSON format

        ```
        {
            "RequestId": "8906582E-6722-409A-A6C4-0E7863B733A5",
            "Code": "UnsupportedOperation",
            "Message": "The specified action is not supported."
        }
        ```

    -   XML format

        ```
        <? xml version="1.0" encoding="UTF-8"? >
        <Error>
           <RequestId>8906582E-6722-409A-A6C4-0E7863B733A5</RequestId>
           <Code>UnsupportedOperation</Code>
           <Message>The specified action is not supported.</Message>
        </Error>
        ```


