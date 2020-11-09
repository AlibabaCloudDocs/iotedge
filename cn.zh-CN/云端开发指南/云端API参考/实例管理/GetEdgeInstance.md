# GetEdgeInstance

调用该接口获取边缘实例详情。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetEdgeInstance|系统规定参数。取值：GetEdgeInstance。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|BizEnable|Boolean|true|边缘实例是否开启。

 -   true：开启。
-   false：关闭。 |
|GmtCreate|String|2019-06-26 12:33:25|创建边缘实例的时间。 |
|GmtCreateTimestamp|Long|1581912859713|创建边缘实例的Unix时间戳。 |
|GmtModified|String|2019-06-26 12:33:25|最后一次更新边缘实例的时间。 |
|GmtModifiedTimestamp|Long|1581912859713|最后一次更新边缘实例的Unix时间戳。 |
|InstanceId|String|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。 |
|LatestDeploymentStatus|Integer|2|边缘实例最近一次部署单的状态。

 -   0：未开始（init）。
-   1：正在进行（processing）。
-   2：成功（success）。
-   3：失败（failure）。 |
|LatestDeploymentType|String|deploy|边缘实例最近一次部署单的类型。

 -   deploy：部署。
-   reset：重置。 |
|Name|String|测试实例new|边缘实例名称。 |
|RoleArn|String|acs:ram::1473922805\*\*\*\*\*\*:role/aliyuniotaccessingfcrole|授权角色的全局资源描述符。 |
|RoleAttachTime|String|2020-02-19 11:25:48|角色绑定时间。 |
|RoleAttachTimestamp|Long|1581912859713|角色绑定的Unix时间戳。 |
|RoleName|String|AliyunIOTAccessingFCRole|授权角色名称。 |
|Spec|Integer|30|产品规格。

 -   10：轻量版。
-   20：标准版。
-   30：专业版。 |
|Tags|String|k1:v1,k2:v2|边缘实例标签，标签由`key:value`组成，多个标签以英文逗号隔开，例如`k1:v1,k2:v2`。 |
|Type|String|0|边缘实例授权类型。

 -   0：自有实例
-   1：授权实例 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|16645053-546B-4D7C-832E-E519B0E23CF1|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=GetEdgeInstance
&InstanceId=F3APY0tPLhmgGtx0****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetEdgeInstanceResponse>
    <RequestId>16645053-546B-4D7C-832E-E519B0E23CF1</RequestId>
    <Data>
        <GmtCreate>2019-06-26 12:33:25</GmtCreate>
        <BizEnable>true</BizEnable>
        <InstanceId>F3APY0tPLhmgGtx0****</InstanceId>
        <LatestDeploymentType>deploy</LatestDeploymentType>
        <GmtModified>2019-06-26 16:16:22</GmtModified>
        <Spec>30</Spec>
        <Tags>k1:v1,k2:v2</Tags>
        <Name>测试实例new</Name>
        <LatestDeploymentStatus>2</LatestDeploymentStatus>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</GetEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "16645053-546B-4D7C-832E-E519B0E23CF1",
  "Data": {
    "GmtCreate": "2019-06-26 12:33:25",
    "BizEnable": true,
    "InstanceId": "F3APY0tPLhmgGtx0****",
    "LatestDeploymentType": "deploy",
    "GmtModified": "2019-06-26 16:16:22",
    "Spec": 30,
    "Tags": "k1:v1,k2:v2",
    "Name": "测试实例new",
    "LatestDeploymentStatus": 2
  },
  "Code": "Success",
  "Success": true
}
```

