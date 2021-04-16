# GetTSL

使用该接口获取指定产品的物模型数据。

## 请求语法

```
GET /2020-04-30/tsls/ProdcutKey HTTP/1.1
Cookie: Cookie
```

**说明：** 其中，`2020-04-30`是边缘端OpenAPI的版本号，请勿修改。

## 请求参数

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|ProductKey|String|是|设备所属产品的唯一标识符。|
|Cookie|String|是|调用[CreateAuthCookie](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/身份认证/CreateAuthCookie.md)接口创建的认证Cookie。|

## 返回语法

```
HTTP/1.1 StatusCode
Content-Type: application/json

Payload
```

## 返回参数

|参数名称|类型|描述|
|----|--|--|
|StatusCode|Number|HTTP状态码。返回200表示成功，返回其它状态码表示失败。状态码详情，请参见[状态码](/cn.zh-CN/物联网边缘计算（旧版本）/边缘端开发指南/边缘端OpenAPI/状态码.md)。|
|Payload|JSON|已获取的产品物模型信息，格式请参见表格下方Payload格式。|

返回Payload格式如下所示。

```
{   
    "Data": {
      "TSL": {}
    }
  }
```

## 完整示例

```
$ curl -i -b token.cookie -k https://127.0.0.1:9999/2020-04-30/tsls/a1t****n42K

HTTP/1.1 200 OK
Server: openresty/1.13.6.2
Date: Tue, 21 Apr 2020 13:30:37 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive

{"Data":{"TSL":{"schema":"https://iotx-tsl.oss-ap-southeast-1.aliyuncs.com/schema.json","services":[{"desc":"属性设置","method":"thing.service.property.set","identifier":"set","inputData":[],"required":true,"outputData":[],"name":"set","callType":"async"},{"desc":"属性获取","method":"thing.service.property.get","identifier":"get","inputData":["MeasuredIlluminance"],"required":true,"outputData":[{"dataType":{"type":"double","specs":{"max":"65535","unit":"Lux","step":"0.01","min":"0","unitName":"照度"}},"identifier":"MeasuredIlluminance","name":"光照度检测值"}],"name":"get","callType":"async"}],"profile":{"productKey":"a1t****n42K"},"events":[{"desc":"属性上报","method":"thing.event.property.post","identifier":"post","type":"info","outputData":[{"dataType":{"type":"double","specs":{"max":"65535","unit":"Lux","step":"0.01","min":"0","unitName":"照度"}},"identifier":"MeasuredIlluminance","name":"光照度检测值"}],"name":"post","required":true},{"method":"thing.event.LowIlluminance.post","identifier":"LowIlluminance","type":"alert","outputData":[{"dataType":{"type":"double","specs":{"max":"65535","unit":"lm","min":"0","step":"0.01"}},"identifier":"MeasuredIlluminance","name":"光照度检测值"},{"dataType":{"type":"int","specs":{"max":"50","min":"-50","step":"1"}},"identifier":"int32","name":"整型参数"},{"dataType":{"type":"float","specs":{"max":"50.0","min":"-50.0","step":"0.1"}},"identifier":"float","name":"单精度浮点型参数"},{"dataType":{"type":"double","specs":{"max":"50.0","min":"-50.0","step":"0.1"}},"identifier":"double","name":"双精度浮点型参数"},{"dataType":{"type":"enum","specs":{"1":"1","2":"2"}},"identifier":"enum","name":"枚举类型参数"},{"dataType":{"type":"bool","specs":{"1":"1","0":"0"}},"identifier":"bool","name":"布尔类型参数"},{"dataType":{"type":"text","specs":{"length":"2048"}},"identifier":"text","name":"字符串类型参数"},{"dataType":{"type":"date","specs":[]},"identifier":"date","name":"时间型"},{"dataType":{"type":"array","specs":{"size":"10","item":{"type":"int"}}},"identifier":"array","name":"数组类型参数"}],"name":"光照度低告警","required":false}],"properties":[{"accessMode":"r","dataType":{"type":"double","specs":{"max":"65535","unit":"Lux","step":"0.01","min":"0","unitName":"照度"}},"required":true,"name":"光照度检测值","identifier":"MeasuredIlluminance"}]}}}
```

