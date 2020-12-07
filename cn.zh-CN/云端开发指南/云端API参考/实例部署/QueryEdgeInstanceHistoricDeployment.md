# QueryEdgeInstanceHistoricDeployment

调用该接口查询边缘实例历史部署单记录。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceHistoricDeployment&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceHistoricDeployment|系统规定参数。取值：QueryEdgeInstanceHistoricDeployment。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|InstanceId|String|是|PgEfYupSn6Pvhfkx\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|PageSize|Integer|是|15|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|StartTime|Long|否|1558951998639|查询起始时间。如果不传入起止时间，则查询该实例的全部历史部署记录。 |
|EndTime|Long|否|1561543998639|查询结束时间。如果不传入起止时间，则查询该实例的全部历史部署记录。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|DeploymentList|Array of Deployment| |边缘实例列表。 |
|DeploymentId|String|e4803e566b424fa68e7f4b1c747c\*\*\*\*|部署单ID。 |
|Description|String|deploy\_1561694817061|部署单描述。 |
|GmtCompleted|String|2019-06-28 12:07:16|部署单完成时间。 |
|GmtCompletedTimestamp|Long|1581912859713|部署单完成的Unix时间戳。 |
|GmtCreate|String|2019-06-26 18:12:29|创建部署单时间。 |
|GmtCreateTimestamp|Long|1581912859713|创建部署单的Unix时间戳。 |
|GmtModified|String|2019-06-28 12:07:16|最后一次更新部署单的时间。 |
|GmtModifiedTimestamp|Long|1581912859713|最后一次更新部署单的Unix时间戳。 |
|Status|Integer|2|实例的部署单状态。

 -   0：未开始（init）。
-   1：正在进行中（processing）。
-   2：成功（success）。
-   3：失败（failure）。 |
|Type|String|deploy|部署单类型。

 -   deploy：部署。
-   reset：重置。 |
|PageSize|Integer|2|返回结果中每页显示的记录数量。 |
|Total|Integer|6|总记录数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|C9D9C91B-1B3B-4D84-BE58-68E7B2A989E4|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceHistoricDeployment
&PageSize=15
&EndTime=1561543998639
&InstanceId=PgEfYupSn6Pvhfkx****
&CurrentPage=1
&StartTime=1558951998639
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

