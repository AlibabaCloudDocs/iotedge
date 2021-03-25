# QueryEdgeInstanceHistoricDeployment

Queries the deployment task records of an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceHistoricDeployment&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryEdgeInstanceHistoricDeployment|The operation that you want to perform. Set the value to QueryEdgeInstanceHistoricDeployment. |
|CurrentPage|Integer|Yes|1|The number of the page to return. Pages start from Page 1. |
|InstanceId|String|Yes|PgEfYupSn6Pvhfkx\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance that you want to manage and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|PageSize|Integer|Yes|15|The number of entries to return on each page. Valid values: 1 to 30. Default value: 10. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|StartTime|Long|No|1558951998639|The beginning of the time range to query. If you do not specify the start time and end time, all the deployment task records of the edge instance are queried. |
|EndTime|Long|No|1561543998639|The end of the time range to query. If you do not specify the start time and end time, all the deployment task records of the edge instance are queried. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|CurrentPage|Integer|1|The page number of the returned page. |
|DeploymentList|Array of Deployment| |The list of deployment tasks. |
|DeploymentId|String|e4803e566b424fa68e7f4b1c747c\*\*\*\*|The ID of the deployment task. |
|Description|String|deploy\_1561694817061|The description of the deployment task. |
|GmtCompleted|String|2019-06-28 12:07:16|The time when the deployment task was complete. |
|GmtCompletedTimestamp|Long|1581912859713|The UNIX timestamp when the deployment task was complete. |
|GmtCreate|String|2019-06-26 18:12:29|The time when the deployment task was created. |
|GmtCreateTimestamp|Long|1581912859713|The UNIX timestamp when the deployment task was created. |
|GmtModified|String|2019-06-28 12:07:16|The last time when the deployment task was modified. |
|GmtModifiedTimestamp|Long|1581912859713|The last UNIX timestamp when the deployment task was modified. |
|Status|Integer|2|The status of the deployment task.

 -   0: The task was not started.
-   1: The task was being processed.
-   2: The task was successful.
-   3: The task failed. |
|Type|String|deploy|The type of the deployment task.

 -   deploy: deploys the edge instance.
-   reset: resets the edge instance. |
|PageSize|Integer|2|The number of entries returned per page. |
|Total|Integer|6|The total number of deployment tasks. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|C9D9C91B-1B3B-4D84-BE58-68E7B2A989E4|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=QueryEdgeInstanceHistoricDeployment
&PageSize=15
&EndTime=1561543998639
&InstanceId=PgEfYupSn6Pvhfkx****
&CurrentPage=1
&StartTime=1558951998639
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryEdgeInstanceHistoricDeploymentResponse>
    <RequestId>C9D9C91B-1B3B-4D84-BE58-68E7B2A989E4</RequestId>
    <Data>
        <DeploymentList>
            <Deployment>
                <Status>2</Status>
                <DeploymentId>e4803e566b424fa68e7f4b1c747c****</DeploymentId>
                <GmtCompleted>2019-06-28 12:07:16</GmtCompleted>
                <Type>deploy</Type>
                <GmtCreate>2019-06-28 12:06:57</GmtCreate>
                <Description>deploy_1561694817061</Description>
                <GmtModified>2019-06-28 12:07:16</GmtModified>
            </Deployment>
            <Deployment>
                <Status>2</Status>
                <DeploymentId>9261e308a9504fde9b4cf8462b0b****</DeploymentId>
                <GmtCompleted>2019-06-26 18:12:35</GmtCompleted>
                <Type>deploy</Type>
                <GmtCreate>2019-06-26 18:12:29</GmtCreate>
                <Description>deploy_1561543948874</Description>
                <GmtModified>2019-06-26 18:12:35</GmtModified>
            </Deployment>
        </DeploymentList>
        <PageSize>2</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>6</Total>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceHistoricDeploymentResponse>
```

`JSON` format

```
{
  "RequestId": "C9D9C91B-1B3B-4D84-BE58-68E7B2A989E4",
  "Data": {
    "DeploymentList": [
      {
        "Status": 2,
        "DeploymentId": "e4803e566b424fa68e7f4b1c747c****",
        "GmtCompleted": "2019-06-28 12:07:16",
        "Type": "deploy",
        "GmtCreate": "2019-06-28 12:06:57",
        "Description": "deploy_1561694817061",
        "GmtModified": "2019-06-28 12:07:16"
      },
      {
        "Status": 2,
        "DeploymentId": "9261e308a9504fde9b4cf8462b0b****",
        "GmtCompleted": "2019-06-26 18:12:35",
        "Type": "deploy",
        "GmtCreate": "2019-06-26 18:12:29",
        "Description": "deploy_1561543948874",
        "GmtModified": "2019-06-26 18:12:35"
      }
    ],
    "PageSize": 2,
    "CurrentPage": 1,
    "Total": 6
  },
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

