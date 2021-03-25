# GetEdgeInstanceDeployment

Queries detailed information about a deployment task of an edge instance.

## Limits

Each Alibaba Cloud account can run a maximum of five queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=GetEdgeInstanceDeployment&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetEdgeInstanceDeployment|The operation that you want to perform. Set the value to GetEdgeInstanceDeployment. |
|DeploymentId|String|Yes|9261e308a9504fde9b4cf8462b0b\*\*\*\*|The ID of the deployment task. You can call the [QueryEdgeInstanceHistoricDeployment](~~135275~~) operation to query the ID of a deployment task. |
|InstanceId|String|Yes|PgEfYupSn6Pvhfkx\*\*\*\*|The ID of the edge instance. To obtain the instance ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Edge Instances** page, move the pointer over the name of the edge instance for which you want to query detailed information about a deployment task and obtain the instance ID.

 You can also call the [QueryEdgeInstance](~~135214~~) operation to query the instance ID. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|DeploymentId|String|9261e308a9504fde9b4cf8462b0b\*\*\*\*|The ID of the deployment task. |
|Description|String|deploy\_1561543948874|The description of the deployment task. |
|GmtCompleted|String|2019-06-26 18:12:35|The time when the deployment task was complete. |
|GmtCompletedTimestamp|Long|1581912859713|The UNIX timestamp when the deployment task was complete. |
|GmtCreate|String|2019-06-26 18:12:29|The time when the deployment task was created. |
|GmtCreateTimestamp|Long|1581912859713|The UNIX timestamp when the deployment task was created. |
|GmtModified|String|2019-06-26 18:12:35|The last time when the deployment task was modified. |
|GmtModifiedTimestamp|Long|1581912859713|The last UNIX timestamp when the deployment task was modified. |
|Status|Integer|2|The status of the deployment task.

 -   0: The task was not started.
-   1: The task was being processed.
-   2: The task was successful.
-   3: The task failed. |
|TaskList|Array of Task| |The list of deployment subtasks. |
|GatewayId|String|jQWf3MVgQjMzcwsY\*\*\*\*000101|The ID of the gateway. |
|GmtCompleted|String|2019-06-26 18:12:35|The time when the deployment subtask was complete. |
|GmtCompletedTimestamp|Long|1581912859713|The UNIX timestamp when the deployment subtask was complete. |
|GmtCreate|String|2019-06-26 18:12:29|The time when the deployment subtask was created. |
|GmtCreateTimestamp|Long|1581912859713|The UNIX timestamp when the deployment subtask was created. |
|GmtModified|String|2019-06-26 18:12:35|The last time when the deployment subtask was modified. |
|GmtModifiedTimestamp|Long|1581912859713|The last UNIX timestamp when the deployment subtask was modified. |
|ResourceSnapshotList|Array of ResourceSnapshot| |The list of deployment task snapshots. |
|GmtCompleted|String|2019-06-26 18:12:34|The time when the deployment task snapshot was complete. |
|GmtCompletedTimestamp|Long|1581912859713|The UNIX timestamp when the deployment task snapshot was complete. |
|GmtCreate|String|2019-06-26 18:12:29|The time when the deployment task snapshot was created. |
|GmtCreateTimestamp|Long|1581912859713|The UNIX timestamp when the deployment task snapshot was created. |
|GmtModified|String|2019-06-26 18:12:34|The last time when the deployment task snapshot was modified. |
|GmtModifiedTimestamp|Long|1581912859713|The last UNIX timestamp when the deployment task snapshot was modified. |
|Log|String|\[\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":0,\\"level\\":\\"INFO\\",\\"message\\":\\"init success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543949858\},\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":8,\\"level\\":\\"INFO\\",\\"message\\":\\"assembly success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543951419\},\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":16,\\"level\\":\\"INFO\\",\\"message\\":\\"package success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543952591\},\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":32,\\"level\\":\\"INFO\\",\\"message\\":\\"download success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543954149\}\]|The logs of resource deployment. |
|OperateType|Integer|0|The type of the operation.

 -   0: deploys resources.
-   1: deletes resources. |
|ResourceId|String|device\_config|The ID of the resource. |
|ResourceName|String|device\_config|The name of the resource. |
|ResourceType|String|device\_config|The type of the resource. |
|SnapshotId|String|ab576e84a43043d7840cbcebf4a5\*\*\*\*|The ID of the deployment task snapshot. |
|Stage|Integer|32|The stage of the snapshot task.

 -   0: The snapshot task was in the initial state.
-   8: The snapshot task was being assembled.
-   16: The snapshot task was being packaged.
-   24: The snapshot task was being dispatched.
-   32: The snapshot task was complete. |
|Status|Integer|2|The status of the snapshot task.

 -   0: The snapshot task was not started.
-   1: The snapshot task was being processed.
-   2: The snapshot task was successful.
-   3: The snapshot task failed. |
|Stage|Integer|32|The stage of the deployment subtask.

 -   0: The subtask was not started.
-   8: The subtask was being assembled.
-   16: The subtask was being packaged.
-   24: The subtask was being dispatched.
-   32: The subtask was complete. |
|Status|Integer|2|The status of the deployment subtask.

 -   0: The subtask was in the initial state.
-   1: The subtask was being processed.
-   2: The subtask was successful.
-   3: The subtask failed. |
|TaskId|String|49ea651529014bf8b5645d5f9062\*\*\*\*|The ID of the deployment subtask. |
|Type|String|deploy|The type of the deployment task.

 -   deploy: deploys the edge instance.
-   reset: resets the edge instance. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|6B72291A-9492-445E-81D9-335D2D3E44C0|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=GetEdgeInstanceDeployment
&InstanceId=PgEfYupSn6Pvhfkx****
&DeployId=9261e308a9504fde9b4cf8462b0b****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetEdgeInstanceDeploymentResponse>
    <RequestId>6B72291A-9492-445E-81D9-335D2D3E44C0</RequestId>
    <Data>
        <Status>2</Status>
        <DeploymentId>9261e308a9504fde9b4cf8462b0b****</DeploymentId>
        <GmtCompleted>2019-06-26 18:12:35</GmtCompleted>
        <Type>deploy</Type>
        <GmtCreate>2019-06-26 18:12:29</GmtCreate>
        <Description>deploy_1561543948874</Description>
        <TaskList>
            <Task>
                <Status>2</Status>
                <GmtCompleted>2019-06-26 18:12:35</GmtCompleted>
                <GmtCreate>2019-06-26 18:12:29</GmtCreate>
                <TaskId>49ea651529014bf8b5645d5f9062****</TaskId>
                <ResourceSnapshotList>
                    <ResourceSnapshot>
                        <Status>2</Status>
                        <SnapshotId>ab576e84a43043d7840cbcebf4a5****</SnapshotId>
                        <GmtCompleted>2019-06-26 18:12:34</GmtCompleted>
                        <GmtCreate>2019-06-26 18:12:29</GmtCreate>
                        <Log>[{"resourceId":"device_config","code":"0","stage":0,"level":"INFO","message":"init success","resourceType":"DEVICE_CONFIG","timestamp":1561543949858},{"resourceId":"device_config","code":"0","stage":8,"level":"INFO","message":"assembly success","resourceType":"DEVICE_CONFIG","timestamp":1561543951419},{"resourceId":"device_config","code":"0","stage":16,"level":"INFO","message":"package success","resourceType":"DEVICE_CONFIG","timestamp":1561543952591},{"resourceId":"device_config","code":"0","stage":32,"level":"INFO","message":"download success","resourceType":"DEVICE_CONFIG","timestamp":1561543954149}]</Log>
                        <ResourceId>device_config</ResourceId>
                        <ResourceName>device_config</ResourceName>
                        <GmtModified>2019-06-26 18:12:34</GmtModified>
                        <Stage>32</Stage>
                        <ResourceType>device_config</ResourceType>
                        <OperateType>0</OperateType>
                    </ResourceSnapshot>
                </ResourceSnapshotList>
                <GmtModified>2019-06-26 18:12:35</GmtModified>
                <Stage>32</Stage>
                <GatewayId>jQWf3MVgQjMzcwsY****000101</GatewayId>
            </Task>
        </TaskList>
        <GmtModified>2019-06-26 18:12:35</GmtModified>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</GetEdgeInstanceDeploymentResponse>
```

`JSON` format

```
{
  "RequestId": "6B72291A-9492-445E-81D9-335D2D3E44C0",
  "Data": {
    "Status": 2,
    "DeploymentId": "9261e308a9504fde9b4cf8462b0b****",
    "GmtCompleted": "2019-06-26 18:12:35",
    "Type": "deploy",
    "GmtCreate": "2019-06-26 18:12:29",
    "Description": "deploy_1561543948874",
    "TaskList": [
      {
        "Status": 2,
        "GmtCompleted": "2019-06-26 18:12:35",
        "GmtCreate": "2019-06-26 18:12:29",
        "TaskId": "49ea651529014bf8b5645d5f9062****",
        "ResourceSnapshotList": [
          {
            "Status": 2,
            "SnapshotId": "ab576e84a43043d7840cbcebf4a5****",
            "GmtCompleted": "2019-06-26 18:12:34",
            "GmtCreate": "2019-06-26 18:12:29",
            "Log": "[{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":0,\"level\":\"INFO\",\"message\":\"init success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543949858},{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":8,\"level\":\"INFO\",\"message\":\"assembly success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543951419},{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":16,\"level\":\"INFO\",\"message\":\"package success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543952591},{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":32,\"level\":\"INFO\",\"message\":\"download success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543954149}]",
            "ResourceId": "device_config",
            "ResourceName": "device_config",
            "GmtModified": "2019-06-26 18:12:34",
            "Stage": 32,
            "ResourceType": "device_config",
            "OperateType": 0
          }
        ],
        "GmtModified": "2019-06-26 18:12:35",
        "Stage": 32,
        "GatewayId": "jQWf3MVgQjMzcwsY****000101"
      }
    ],
    "GmtModified": "2019-06-26 18:12:35"
  },
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

