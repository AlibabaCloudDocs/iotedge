# QueryEdgeInstance

调用该接口查询当前账号下的所有边缘实例。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstance|系统规定参数。取值：QueryEdgeInstance。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值是1。 |
|PageSize|Integer|是|15|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |
|Name|String|否|测试实例\_test|边缘实例名称。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|InstanceList|Array of Instance| |边缘实例列表。 |
|BizEnable|Boolean|true|边缘实例是否开启。

 -   true：开启。
-   false：关闭。 |
|GmtCreate|String|2019-07-17 14:34:28|创建边缘实例的时间。 |
|GmtCreateTimestamp|Long|1581912859713|创建边缘实例的Unix时间戳。 |
|GmtModified|String|2019-07-17 14:51:38|最后一次更新边缘实例的时间。 |
|GmtModifiedTimestamp|Long|1581912859713|最后一次更新边缘实例的Unix时间戳。 |
|InstanceId|String|9iqyQAKDb2aYGVKa\*\*\*\*|边缘实例ID。 |
|LatestDeploymentStatus|Integer|1|边缘实例最近一次部署单状态。

 -   0：未开始（init）。
-   1：正在进行（processing）。
-   2：成功（success）。
-   3：失败（failure）。 |
|LatestDeploymentType|String|deploy|边缘实例最近一次部署单类型。

 -   deploy：部署。
-   reset：重置。 |
|Name|String|test\_le1|边缘实例名称。 |
|RoleArn|String|acs:ram::1473922805\*\*\*\*\*\*:role/aliyuniotaccessingfcrole|授权角色的全局资源描述符。 |
|RoleAttachTime|String|2020-02-19 11:25:48|角色绑定时间。 |
|RoleAttachTimestamp|Long|1581912859713|角色绑定的Unix时间戳。 |
|RoleName|String|AliyunIOTAccessingFCRole|授权角色名称。 |
|Spec|Integer|30|产品规格。

 -   10：轻量版。
-   20：标准版。
-   30：专业版。 |
|Tags|String|k1:v1,k2:v2|边缘实例标签。 |
|Type|Integer|0|边缘实例授权类型。

 -   0：自有实例
-   1：授权实例 |
|PageSize|Integer|2|返回结果中每页显示的记录数量。 |
|Total|Integer|201|边缘实例数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|199BBC5D-FC99-46CB-88E2-FB98E92446FA|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstance
&PageSize=15
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryEdgeInstanceResponse>
    <RequestId>199BBC5D-FC99-46CB-88E2-FB98E92446FA</RequestId>
    <Data>
        <PageSize>2</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>201</Total>
        <InstanceList>
            <Instance>
                <GmtCreate>2019-07-17 14:34:28</GmtCreate>
                <BizEnable>true</BizEnable>
                <InstanceId>9iqyQAKDb2aYGVKa****</InstanceId>
                <GmtModified>2019-07-17 14:51:38</GmtModified>
                <Spec>20</Spec>
                <Name>test_le1</Name>
            </Instance>
            <Instance>
                <GmtCreate>2018-10-22 20:09:29</GmtCreate>
                <BizEnable>true</BizEnable>
                <InstanceId>ZpbCxkQpbb2kpmm0****</InstanceId>
                <LatestDeploymentType>reset</LatestDeploymentType>
                <GmtModified>2019-07-16 16:50:50</GmtModified>
                <Spec>30</Spec>
                <Name>test_le1</Name>
                <LatestDeploymentStatus>1</LatestDeploymentStatus>
            </Instance>
        </InstanceList>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "199BBC5D-FC99-46CB-88E2-FB98E92446FA",
  "Data": {
    "PageSize": 2,
    "CurrentPage": 1,
    "Total": 201,
    "InstanceList": [
      {
        "GmtCreate": "2019-07-17 14:34:28",
        "BizEnable": true,
        "InstanceId": "9iqyQAKDb2aYGVKa****",
        "GmtModified": "2019-07-17 14:51:38",
        "Spec": 20,
        "Name": "test_le1"
      },
      {
        "GmtCreate": "2018-10-22 20:09:29",
        "BizEnable": true,
        "InstanceId": "ZpbCxkQpbb2kpmm0****",
        "LatestDeploymentType": "reset",
        "GmtModified": "2019-07-16 16:50:50",
        "Spec": 30,
        "Name": "test_le1",
        "LatestDeploymentStatus": 1
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

