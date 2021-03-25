# GetEdgeInstanceDeployment

调用该接口获取边缘实例部署单详情。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetEdgeInstanceDeployment&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetEdgeInstanceDeployment|系统规定参数。取值：GetEdgeInstanceDeployment。 |
|DeploymentId|String|是|9261e308a9504fde9b4cf8462b0b\*\*\*\*|部署单ID。可调用[QueryEdgeInstanceHistoricDeployment](~~135275~~)接口获取。 |
|InstanceId|String|是|PgEfYupSn6Pvhfkx\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|DeploymentId|String|9261e308a9504fde9b4cf8462b0b\*\*\*\*|部署单ID。 |
|Description|String|deploy\_1561543948874|部署单描述。 |
|GmtCompleted|String|2019-06-26 18:12:35|部署完成时间。 |
|GmtCompletedTimestamp|Long|1581912859713|部署完成的Unix时间戳。 |
|GmtCreate|String|2019-06-26 18:12:29|部署单创建时间。 |
|GmtCreateTimestamp|Long|1581912859713|部署单创建的Unix时间戳。 |
|GmtModified|String|2019-06-26 18:12:35|部署单最后一次更新时间。 |
|GmtModifiedTimestamp|Long|1581912859713|部署单最后一次更新的Unix时间戳。 |
|Status|Integer|2|部署单当前状态。

 -   0：未开始（init）。
-   1：正在进行中（processing）。
-   2：成功（success）。
-   3：失败（failure）。 |
|TaskList|Array of Task| |部署任务列表。 |
|GatewayId|String|jQWf3MVgQjMzcwsY\*\*\*\*000101|网关设备ID。 |
|GmtCompleted|String|2019-06-26 18:12:35|部署任务完成时间。 |
|GmtCompletedTimestamp|Long|1581912859713|部署任务完成的Unix时间戳。 |
|GmtCreate|String|2019-06-26 18:12:29|部署任务创建时间。 |
|GmtCreateTimestamp|Long|1581912859713|部署任务创建的Unix时间戳。 |
|GmtModified|String|2019-06-26 18:12:35|部署任务最后一次更新时间。 |
|GmtModifiedTimestamp|Long|1581912859713|部署任务最后一次更新的Unix时间戳。 |
|ResourceSnapshotList|Array of ResourceSnapshot| |部署快照列表。 |
|GmtCompleted|String|2019-06-26 18:12:34|部署单快照完成时间。 |
|GmtCompletedTimestamp|Long|1581912859713|部署单快照完成的Unix时间戳。 |
|GmtCreate|String|2019-06-26 18:12:29|部署单快照创建时间。 |
|GmtCreateTimestamp|Long|1581912859713|部署单快照创建的Unix时间戳。 |
|GmtModified|String|2019-06-26 18:12:34|部署单快照最后一次更新时间。 |
|GmtModifiedTimestamp|Long|1581912859713|部署单快照最后一次更新的Unix时间戳。 |
|Log|String|\[\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":0,\\"level\\":\\"INFO\\",\\"message\\":\\"init success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543949858\},\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":8,\\"level\\":\\"INFO\\",\\"message\\":\\"assembly success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543951419\},\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":16,\\"level\\":\\"INFO\\",\\"message\\":\\"package success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543952591\},\{\\"resourceId\\":\\"device\_config\\",\\"code\\":\\"0\\",\\"stage\\":32,\\"level\\":\\"INFO\\",\\"message\\":\\"download success\\",\\"resourceType\\":\\"DEVICE\_CONFIG\\",\\"timestamp\\":1561543954149\}\]|资源部署日志。 |
|OperateType|Integer|0|操作类型。

 -   0：部署（deploy）。
-   1：删除（delete）。 |
|ResourceId|String|device\_config|资源ID。 |
|ResourceName|String|device\_config|资源名称。 |
|ResourceType|String|device\_config|资源类型。 |
|SnapshotId|String|ab576e84a43043d7840cbcebf4a5\*\*\*\*|部署快照ID。 |
|Stage|Integer|32|部署单快照当前阶段。

 -   0：初始状态（init）。
-   8：正在编译（assembly）。
-   16：正在打包（package）。
-   24：正在分发（dispatcher）。
-   32：已完成（finish）。 |
|Status|Integer|2|当前状态。

 -   0：未开始（init）。
-   1：正在进行（processing）。
-   2：成功（success）。
-   3：失败（failure）。 |
|Stage|Integer|32|部署任务当前阶段。

 -   0：未开始（init）。
-   8：正在装配（assembly）。
-   16：正在打包（package）。
-   24：正在分发（dispatcher）。
-   32：已完成（finish）。 |
|Status|Integer|2|部署任务当前状态。

 -   0：初始状态（init）。
-   1：正在进行中（processing）。
-   2：成功（success）。
-   3：失败（failure）。 |
|TaskId|String|49ea651529014bf8b5645d5f9062\*\*\*\*|部署任务ID。 |
|Type|String|deploy|部署单类型。

 -   deploy：部署。
-   reset：重置。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|6B72291A-9492-445E-81D9-335D2D3E44C0|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=GetEdgeInstanceDeployment
&InstanceId=PgEfYupSn6Pvhfkx****
&DeployId=9261e308a9504fde9b4cf8462b0b****
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

