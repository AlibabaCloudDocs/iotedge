# QueryEdgeInstanceDriver

Queries the drivers that are bound to an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceDriver&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryEdgeInstanceDriver|The operation that you want to perform. Set the value to QueryEdgeInstanceDriver. |
|CurrentPage|Integer|Yes|1|The number of the page to return. Pages start from Page 1. |
|InstanceId|String|Yes|F3APY0tPLhmgGtx0\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that you want to query and obtain the instance ID.

You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|PageSize|Integer|Yes|10|The number of entries to return on each page. Valid values: 1 to 30. Default value: 10. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|CurrentPage|Integer|1|The page number of the returned page. |
|DriverList|Array of Driver| |The list of drivers. |
|DriverId|String|9c1ae7bd59f1469abbdccc959228\*\*\*\*|The ID of the driver. |
|DriverVersion|String|1.0.0|The version number of the driver. |
|GmtCreate|String|2019-06-26 17:22:25|The time when the driver was created. |
|GmtModified|String|2019-06-26 17:22:25|The last time when the driver was updated. |
|OrderId|String|11123458765423|The ID of the order. |
|PageSize|Integer|30|The number of entries returned per page. |
|Total|Integer|1|The number of drivers. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|77F540BC-A0EF-46A4-ABDE-18644C69AAF5|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=QueryEdgeInstanceDriver
&PageSize=30
&InstanceId=F3APY0tPLhmgGtx0****
&CurrentPage=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryEdgeInstanceDriverResponse>
    <RequestId>77F540BC-A0EF-46A4-ABDE-18644C69AAF5</RequestId>
    <Data>
        <PageSize>30</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>1</Total>
        <DriverList>
            <Driver>
                <GmtCreate>2019-06-26 17:22:25</GmtCreate>
                <DriverId>9c1ae7bd59f1469abbdccc959228****</DriverId>
                <GmtModified>2019-06-26 17:22:25</GmtModified>
            </Driver>
        </DriverList>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceDriverResponse>
```

`JSON` format

```
{
  "RequestId": "77F540BC-A0EF-46A4-ABDE-18644C69AAF5",
  "Data": {
    "PageSize": 30,
    "CurrentPage": 1,
    "Total": 1,
    "DriverList": [
      {
        "GmtCreate": "2019-06-26 17:22:25",
        "DriverId": "9c1ae7bd59f1469abbdccc959228****",
        "GmtModified": "2019-06-26 17:22:25"
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

