# QueryEdgeInstanceMessageRouting

调用该接口，分页查询边缘实例中的消息路由。

## 限制条件

-   如果在企业版实例中调用该接口，必须传入参数**IotInstanceId**的值。否则，调用接口会失败。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryEdgeInstanceMessageRouting&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryEdgeInstanceMessageRouting|系统规定参数。取值：QueryEdgeInstanceMessageRouting。 |
|CurrentPage|Integer|是|1|指定从返回结果中的第几页开始显示。最小取值为1。 |
|InstanceId|String|是|UMJH812PQgJ8\*\*\*\*\*\*\*\*|边缘实例ID。在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)的**边缘实例**页面中，鼠标指针悬浮在目标边缘实例名称上获取ID。 |
|PageSize|Integer|是|15|返回结果中，每页显示的记录数量。最大取值30，最小取值1，默认取值为10。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|物联网平台的实例ID：

 -   企业版实例：必须传入此参数。您可在[物联网平台控制台](http://iot.console.aliyun.com/)的**实例概览**页面，查看您的企业版实例ID。
-   公共实例：无需传入此参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~135196~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|接口返回码：

 -   **Success**：表示成功。
-   其它：表示错误码。错误码详情，请参见[错误码](~~135200~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|CurrentPage|Integer|1|当前页码。 |
|MessageRouteList|Array of MessageRoute| |消息路由列表。 |
|MessageRoute| | | |
|GmtCreate|String|2021-04-15 19:39:20|创建消息路由的时间。 |
|GmtCreateTimestamp|Long|1618486760000|创建消息路由的Unix时间戳。 |
|GmtModified|String|2021-04-15 19:47:10|最后一次更新消息路由的时间。 |
|GmtModifiedTimestamp|Long|1618487230000|最后一次更新消息路由的Unix时间戳。 |
|Name|String|sample|消息路由名称。 |
|RouteContext|Struct| |消息来源和消息接收者的补充信息。 |
|Qos|String|0|服务级别：

 -   0：表示消息仅发送一次，不管是否被消息接收者成功接收。
-   1：表示最少发送一次消息，直至收到消息接收者的返回信息，则停止发送该消息。 |
|SourceApplicationName|String|le\_object\_detector|**SourceType**为**function**，且**SourceData**中指定的边缘应用，是函数计算类型的边缘应用时，返回此参数，表示函数计算类型边缘应用的名称。 |
|SourceFcFunctionName|String|object\_detector\_app|**SourceType**为**function**，且**SourceData**中指定的边缘应用，是函数计算类型的边缘应用时，返回此参数，表示函数计算类型边缘应用中的函数名称。 |
|SourceFcServiceName|String|EdgeFC|**SourceType**为**function**，且**SourceData**中指定的边缘应用，是函数计算类型的边缘应用时，返回此参数，表示函数计算类型边缘应用中的服务名称。 |
|TargetApplicationName|String|le\_object\_detector|**TargetType**为**function**，且**TargetData**中指定的边缘应用，是函数计算类型的边缘应用时，返回此参数，表示函数计算类型边缘应用的名称。 |
|TargetFcFunctionName|String|lightSensorDataFilter|**TargetType**为**function**，且**TargetData**中指定的边缘应用，是函数计算类型的边缘应用时，返回此参数，表示函数计算类型边缘应用中的函数名称。 |
|TargetFcServiceName|String|EdgeFC|**TargetType**为**function**，且**TargetData**中指定的边缘应用，是函数计算类型的边缘应用时，返回此参数，表示函数计算类型边缘应用中的服务名称。 |
|RouteId|Integer|123456|消息路由ID。 |
|SourceData|String|/a127n\*\*\*\*\*\*/test1098|消息来源的数据：

 -   **SourceType**为**device**时：
    -   此处参数值格式为`/{Your_ProductKey}/{Your_DeviceName}`：表示消息来源为指定产品下的指定设备。

**说明：** \{Your\_ProductKey\}和\{Your\_DeviceName\}是您实际设备的ProductKey和DeviceName。

    -   此处参数值格式为`/{Your_ProductKey}/+`：表示消息来源为指定产品下的所有设备。

**说明：** \{Your\_ProductKey\}是您实际设备的ProductKey。

    -   此处参数值为**\#**：表示消息来源为边缘实例中所有产品下的所有设备。
-   **SourceType**为**function**时：此处是边缘应用的ID。
-   **SourceType**为**IotHub**时：此处为空。 |
|SourceType|String|device|消息来源：

 -   **device**：表示消息由设备发出。
-   **function**：表示消息由边缘应用发出。
-   **IotHub**：表示消息由云端发出。 |
|TargetData|String|58c46749ac934db3925fe5\*\*\*\*\*\*\*\*|消息接收者的数据：

 -   **TargetType**为**function**时：此处是边缘应用的ID。
-   **TargetType**为**IotHub**时：此处为空。 |
|TargetType|String|IotHub|消息接收者：

 -   **function**：表示消息发送给边缘应用。
-   **IotHub**：表示消息发送给云端。 |
|TopicFilter|String|all|消息过滤条件。 |
|PageSize|Integer|15|返回结果中每页显示的记录数量。 |
|Total|Integer|2|消息路由总数。 |
|ErrorMessage|String|request parameter error|调用失败时，返回的出错信息。 |
|RequestId|String|8A248DEC-887C-4A37-8DE5-E128FFA3698D|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功：

 -   **true**：表示调用成功。
-   **false**：表示调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceMessageRouting
&instanceId=UMJH812PQgJ8********
&regionId=cn-shanghai
&pageSize=15
&currentPage=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<QueryEdgeInstanceMessageRoutingResponse>
    <RequestId>8A248DEC-887C-4A37-8DE5-E128FFA3698D</RequestId>
    <Data>
        <PageSize>15</PageSize>
        <CurrentPage>1</CurrentPage>
        <Total>2</Total>
        <MessageRouteList>
            <MessageRoute>
                <TargetData></TargetData>
                <TopicFilter>all</TopicFilter>
                <GmtCreate>2021-04-15 19:39:20</GmtCreate>
                <GmtCreateTimestamp>1618486760000</GmtCreateTimestamp>
                <SourceType>device</SourceType>
                <TargetType>IotHub</TargetType>
                <GmtModified>2021-04-15 19:47:10</GmtModified>
                <RouteId>123456</RouteId>
                <GmtModifiedTimestamp>1618487230000</GmtModifiedTimestamp>
                <SourceData>/a127n******/test1098</SourceData>
                <Name>sample</Name>
                <RouteContext>
                    <Qos>1</Qos>
                </RouteContext>
            </MessageRoute>
            <MessageRoute>
                <TargetData></TargetData>
                <TopicFilter>all</TopicFilter>
                <GmtCreate>2020-05-25 19:54:59</GmtCreate>
                <GmtCreateTimestamp>1590407699000</GmtCreateTimestamp>
                <SourceType>device</SourceType>
                <TargetType>IotHub</TargetType>
                <GmtModified>2020-05-25 19:54:59</GmtModified>
                <RouteId>170101</RouteId>
                <GmtModifiedTimestamp>1590407699000</GmtModifiedTimestamp>
                <SourceData>#</SourceData>
                <RouteContext>
                    <Qos>0</Qos>
                </RouteContext>
            </MessageRoute>
        </MessageRouteList>
    </Data>
    <Code>Success</Code>
    <Success>true</Success>
</QueryEdgeInstanceMessageRoutingResponse>
```

`JSON`格式

```
{
  "RequestId": "8A248DEC-887C-4A37-8DE5-E128FFA3698D",
  "Data": {
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 2,
    "MessageRouteList": {
      "MessageRoute": [
        {
          "TargetData": "",
          "TopicFilter": "all",
          "GmtCreate": "2021-04-15 19:39:20",
          "GmtCreateTimestamp": 1618486760000,
          "SourceType": "device",
          "TargetType": "IotHub",
          "GmtModified": "2021-04-15 19:47:10",
          "RouteId": 123456,
          "GmtModifiedTimestamp": 1618487230000,
          "SourceData": "/a127n******/test1098",
          "Name": "sample",
          "RouteContext": {
            "Qos": 1
          }
        },
        {
          "TargetData": "",
          "TopicFilter": "all",
          "GmtCreate": "2020-05-25 19:54:59",
          "GmtCreateTimestamp": 1590407699000,
          "SourceType": "device",
          "TargetType": "IotHub",
          "GmtModified": "2020-05-25 19:54:59",
          "RouteId": 170101,
          "GmtModifiedTimestamp": 1590407699000,
          "SourceData": "#",
          "RouteContext": {
            "Qos": 0
          }
        }
      ]
    }
  },
  "Code": "Success",
  "Success": true
}
```

