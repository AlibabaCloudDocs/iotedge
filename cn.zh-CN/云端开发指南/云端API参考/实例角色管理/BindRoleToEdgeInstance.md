# BindRoleToEdgeInstance

调用该接口将角色绑定到边缘实例。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BindRoleToEdgeInstance&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BindRoleToEdgeInstance|系统规定参数。取值：BindRoleToEdgeInstance。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|RoleArn|String|是|acs:ram::176\*\*\*\*\*\*\*\*:role/iotedgerole|授权角色的全局资源描述符（ARN）。在[RAM控制台](https://ram.console.aliyun.com/)创建角色后，单击角色名，可在**基本信息**页查看其ARN。 |
|RoleName|String|是|IoTEdgeRole|角色名称。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|3DE428F8-22AF-4B37-8FEC-E64CFBE4A125|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BindRoleToEdgeInstance
&RoleName=IoTEdgeRole
&InstanceId=F3APY0tPLhmgGtx0****
&RoleArn=acs:ram::176********:role/iotedgerole
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BindRoleToEdgeInstanceResponse>
    <RequestId>3DE428F8-22AF-4B37-8FEC-E64CFBE4A125</RequestId>
    <Code>Success</Code>
    <Success>true</Success>
</BindRoleToEdgeInstanceResponse>
```

`JSON` 格式

```
{
  "RequestId": "3DE428F8-22AF-4B37-8FEC-E64CFBE4A125",
  "Code": "Success",
  "Success": true
}
```

