# QueryEdgeInstanceDriver

调用该接口查询边缘实例的驱动列表。

## 限制条件

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享主账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceDriver&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceDriver|系统规定参数。取值：QueryEdgeInstanceDriver。 |
|CurrentPage|Integer|是|1|从返回结果中的第几页开始显示。最小取值为1。 |
|InstanceId|String|是|F3APY0tPLhmgGtx0\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标悬浮在目标边缘实例名称上获取ID。

 您也可以调用[QueryEdgeInstance](~~135214~~)接口获取。 |
|PageSize|Integer|是|10|返回结果中每页显示的记录数量。最大取值30，最小取值1，默认取值是10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|公共实例不传此参数；您购买的实例需传入实例ID。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码。Success表示成功，其它表示错误码。详情请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|DriverList|Array of Driver| |驱动列表。 |
|DriverId|String|9c1ae7bd59f1469abbdccc959228\*\*\*\*|驱动ID。 |
|DriverVersion|String|1.0.0|驱动版本号。 |
|GmtCreate|String|2019-06-26 17:22:25|驱动创建时间。 |
|GmtModified|String|2019-06-26 17:22:25|驱动最后一次更新时间。 |
|OrderId|String|11123458765423|订单编号。 |
|PageSize|Integer|30|返回结果中每页显示的记录数量。 |
|Total|Integer|1|驱动数量。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|77F540BC-A0EF-46A4-ABDE-18644C69AAF5|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。true表示调用成功，false表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceDriver
&PageSize=30
&InstanceId=F3APY0tPLhmgGtx0****
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

