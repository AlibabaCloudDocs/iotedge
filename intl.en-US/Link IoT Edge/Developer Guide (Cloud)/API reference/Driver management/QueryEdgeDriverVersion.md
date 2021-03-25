# QueryEdgeDriverVersion

Queries the versions of a driver by page.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryEdgeDriverVersion&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryEdgeDriverVersion|The operation that you want to perform. Set the value to QueryEdgeDriverVersion. |
|CurrentPage|Integer|Yes|1|The number of the page to return. Pages start from Page 1. |
|DriverId|String|Yes|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|The ID of the driver. To obtain the driver ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of the driver whose versions you want to query and obtain the driver ID.

 You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver ID. |
|PageSize|Integer|Yes|15|The number of entries to return on each page. Valid values: 1 to 30. Default value: 10. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|DriverVersion|String|No|LED driver|The version number of the driver. To query information about a specific driver version, set this parameter to the specific version number. |
|VersionState|Integer|No|0|The status of the driver version. Valid values:

 -   0: The driver version to be queried is not published.
-   1: The driver version to be queried is published. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~135196~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|Data|Struct| |The data that is returned if the call was successful. |
|CurrentPage|Integer|1|The page number of the returned page. |
|DriverVersionList|Array of DriverVersion| |The information about each version of the driver. |
|Argument|String|-XX:+PrintGCDetails|The Java Virtual Machine \(JVM\) startup parameter. |
|ConfigCheckRule|String|\{\\"deviceConfig\\":\{\\"required\\":false\},\\"driverConfig\\":\{\\"required\\":false\}\}|The rule for verifying configurations. The value is a JSON string in the following format:

 `{"deviceConfig":{"required":false},"driverConfig":{"required":false}` The JSON string contains the following parameters:

 -   driverConfig: the rule for verifying the configuration of the driver when the driver is to be deployed in an edge instance.
-   deviceConfig: the rule for verifying the configurations of devices that use the driver when the driver is to be deployed in an edge instance. |
|ContainerConfig|String|\{\\"devMappings\\":\[\],\\"hostNetworkMode\\":0,\\"portMappings\\":\[\],\\"privileged\\":1,\\"volumeMappings\\":\[\]\}|The configuration of the container where the driver runs. The value is a JSON string. For more information about parameters in the JSON string, see the following parameter description of ContainerConfig. |
|Description|String|LED driver|The description of the driver. |
|DriverConfig|String|\[\{\\"content\\":\\"\{\\\\\\"defaultConfig\\\\\\":\\\\\\"this is default driver config demo\\\\\\"\}\\",\\"format\\":\\"JSON\\"\}\]|The configuration of the driver. The value is a JSON string in the following format:

 `{"format":"JSON","content":"{}"}` The JSON string contains the following parameters:

 -   format: the format of the driver configuration. Valid values: KV \(key-value pair\), JSON \(JSON string\), and FILE \(configuration file\).
-   content: the content of the driver configuration. If the format parameter is set to KV or JSON, the value of this parameter is the configuration content. If the format parameter is set to FILE, the value of this parameter is the URL of the configuration file stored in Object Storage Service \(OSS\). |
|DriverId|String|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|The ID of the driver. |
|DriverVersion|String|1.2.0|The version number of the driver. |
|EdgeVersion|String|2.0.0|The earliest version of Link IoT Edge that is supported by the driver. |
|GmtCreateTimestamp|Long|1581912859713|The UNIX timestamp when the driver was created. |
|GmtModifiedTimestamp|Long|1581912859713|The last UNIX timestamp when the driver was updated. |
|SourceConfig|String|\{\\"ossAddress\\":\\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3\*\*\*\*\*\*/ck3n3koe200003h6zf\*\*\*\*\*\*.zip\\",\\"temporaryOssAddress\\":\\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3\*\*\*\*\*\*/ck3n3koe200003h6zf\*\*\*\*\*\*.zip?Expires\\u003d1575\*\*\*\*\*\*\\u0026OSSAccessKeyId\\u003daS4MT0IYr\*\*\*\*\*\*\\u0026Signature\\u003dm6cpmcaB8rm3YfbkhTYgb0W\*\*\*\*\*\*\\"\}|The source of the driver code. The value is a JSON string in the following format:

 `{"ossAddress":"http://***/driver_code.zip","temporaryOssAddress":"http://***/driver_code.zip?Expires***"}` In the JSON string, `ossAddress` indicates the URL of the driver code stored in OSS and `temporaryOssAddress` indicates the temporary link for downloading the driver code. The validity period of the temporary link is 5 minutes. |
|VersionState|String|0|The status of the driver version. Valid values:

 -   0: The driver version was not published.
-   1: The driver version was published. |
|PageSize|Integer|15|The number of entries returned per page. |
|Total|Integer|1|The number of driver versions. |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|ABA0CD1F-4270-42FE-84AD-D612240196F7|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

**Parameter description of ContainerConfig**

|Parameter

|Type

|Description |
|-----------|------|-------------|
|privileged

|Integer

|Indicates whether the privilege mode was enabled for the container. Valid values:

 0: disabled

 1: enabled |
|hostNetworkMode

|Integer

|Indicates whether the host mode was enabled for the container. Valid values:

 0: disabled

 1: enabled |
|portMappings

|List

|The mapping of network ports. For more information about specific parameters, see the following parameter description of portMappings. |
|devMappings

|List

|The mapping of devices. For more information about specific parameters, see the following parameter description of devMappings. |
|volumeMappings

|List

|The mapping of volumes. For more information about specific parameters, see the following parameter description of volumeMappings. |

**Parameter description of portMappings**

|Parameter

|Type

|Description |
|-----------|------|-------------|
|hostPort

|Integer

|The port number of the host where the container resides. |
|containerPort

|Integer

|The port number of the container. |
|protocol

|Integer

|The type of the protocol that is used for communication between the mapping ports. Valid values: tcp and udp. |

**Parameter description of devMappings**

|Parameter

|Type

|Description |
|-----------|------|-------------|
|hostPath

|String

|The name of the device that the driver needs to access. |
|permission

|String

|The permissions that the driver has for the device. Valid values:

 ro: The driver has only the read permissions for the device.

 rw: The driver has both the read and write permissions for the device. |
|comment

|String

|The remarks for the mapping. |

**Parameter description of volumeMappings**

|Parameter

|Type

|Description |
|-----------|------|-------------|
|hostPath

|String

|The host path of the volume that the driver needs to access. |
|containerPath

|String

|The path for accessing the volume in the container. |
|permission

|String

|The permissions that the driver has for the volume. Valid values:

 ro: The driver has only the read permissions for the volume.

 rw: The driver has both the read and write permissions for the volume. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=QueryEdgeDriverVersion
&DriverId=fec565038d7544978d9aed5c1a******
&PageSize=15
&CurrentPage=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryEdgeDriverVersionResponse>
      <RequestId>ABA0CD1F-4270-42FE-84AD-D612240196F7</RequestId>
      <Data>
            <PageSize>15</PageSize>
            <CurrentPage>1</CurrentPage>
            <Total>1</Total>
            <DriverVersionList>
                  <DriverVersion>
                        <ContainerConfig>{"devMappings":[],"hostNetworkMode":0,"portMappings":[],"privileged":1,"volumeMappings":[]}</ContainerConfig>
                        <GmtCreate>2019-12-01 22:28:01</GmtCreate>
                        <DriverId>fec565038d7544978d9aed5c1a******</DriverId>
                        <Description>LED driver</Description>
                        <DriverVersion>1.2.0</DriverVersion>
                        <SourceConfig>{"ossAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30******/ck3n3koe200003h6zf******.zip","temporaryOssAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30******/ck3n3koe200003h6zf******.zip?Expires=1575******&amp;OSSAccessKeyId=aS4MT0IYrPS******&amp;Signature=m6cpmcaB8rm3YfbkhTYgb0WO******"}</SourceConfig>
                        <GmtModified>2019-12-01 22:28:01</GmtModified>
                        <DriverConfig>[{"content":"{\"defaultConfig\":\"this is default driver config demo\"}","format":"JSON"}]</DriverConfig>
                        <EdgeVersion>2.0.0</EdgeVersion>
                        <ConfigCheckRule>{"deviceConfig":{"required":false},"driverConfig":{"required":false}}</ConfigCheckRule>
                        <VersionState>0</VersionState>
                  </DriverVersion>
            </DriverVersionList>
      </Data>
      <Code>Success</Code>
      <Success>true</Success>
</QueryEdgeDriverVersionResponse>
```

`JSON` format

```
{
  "RequestId": "ABA0CD1F-4270-42FE-84AD-D612240196F7",
  "Data": {
    "PageSize": 15,
    "CurrentPage": 1,
    "Total": 1,
    "DriverVersionList": [
      {
        "ContainerConfig": "{\"devMappings\":[],\"hostNetworkMode\":0,\"portMappings\":[],\"privileged\":1,\"volumeMappings\":[]}",
        "GmtCreate": "2019-12-01 22:28:01",
        "DriverId": "fec565038d7544978d9aed5c1a******",
        "Description": "LED driver",
        "DriverVersion": "1.2.0",
        "SourceConfig": "{\"ossAddress\":\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3******/ck3n3koe200003h6zf******.zip\",\"temporaryOssAddress\":\"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb3******/ck3n3koe200003h6zf******.zip?Expires\u003d1575******\u0026OSSAccessKeyId\u003daS4MT0IYr******\u0026Signature\u003dm6cpmcaB8rm3YfbkhTYgb0W******\"}",
        "GmtModified": "2019-12-01 22:28:01",
        "DriverConfig": "[{\"content\":\"{\\\"defaultConfig\\\":\\\"this is default driver config demo\\\"}\",\"format\":\"JSON\"}]",
        "EdgeVersion": "2.0.0",
        "ConfigCheckRule": "{\"deviceConfig\":{\"required\":false},\"driverConfig\":{\"required\":false}}",
        "VersionState": 0
      }
    ]
  },
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

