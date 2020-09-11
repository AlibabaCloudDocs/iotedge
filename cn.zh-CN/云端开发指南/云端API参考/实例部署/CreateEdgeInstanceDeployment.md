# CreateEdgeInstanceDeployment

调用该接口创建边缘实例部署单。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** 子账号共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateEdgeInstanceDeployment&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateEdgeInstanceDeployment|系统规定参数。取值：CreateEdgeInstanceDeployment。 |
|InstanceId|String|是|PgEfYupSn6Pvhfkx\*\*\*\*|边缘实例ID。在物联网平台控制台的**边缘计算** \> **边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|Type|String|是|deploy|部署单类型。

 -   deploy：部署。
-   reset：重置。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|DeploymentId|String|38d544b1222d45b4b425240167bf\*\*\*\*|调用成功时，返回的部署任务单ID。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|C8293A57-6BBC-42FB-B093-BF304D5BF09C|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeInstanceDeployment
&InstanceId=PgEfYupSn6Pvhfkx****
&Type=deploy
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateEdgeInstanceDeploymentResponse>
    <RequestId>C8293A57-6BBC-42FB-B093-BF304D5BF09C</RequestId>
    <DeploymentId>38d544b1222d45b4b425240167bf****</Data>
    <Code>Success</Code>
    <Success>true</Success>
</CreateEdgeInstanceDeploymentResponse>
```

`JSON` 格式

```
{
  "RequestId": "C8293A57-6BBC-42FB-B093-BF304D5BF09C",
  "DeploymentId": "38d544b1222d45b4b425240167bf****",
  "Code": "Success",
  "Success": true
}
```

