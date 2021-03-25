# CreateEdgeDriverVersion

Creates a driver version.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateEdgeDriverVersion&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateEdgeDriverVersion|The operation that you want to perform. Set the value to CreateEdgeDriverVersion. |
|DriverId|String|Yes|fec565038d7544978d9aed5c1a\*\*\*\*\*\*|The ID of the driver. To obtain the driver ID, perform the following steps: Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). On the **Drivers** page, move the pointer over the name of the driver for which you want to create a driver version and obtain the driver ID.

 You can also call the [QueryEdgeDriver](~~155776~~) operation to query the driver ID. |
|DriverVersion|String|Yes|1.2.0|The version number of the driver. The version number must be unique for the driver. The version number can be up to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). |
|EdgeVersion|String|Yes|2.0.0|The earliest version of Link IoT Edge that is supported by the driver. The driver can run on gateways of only this version and later. For example, if you set this parameter to 2.4.0, the driver can run on gateways of only version 2.4.0 and later. |
|Argument|String|No|-XX:+PrintGCDetails|The Java Virtual Machine \(JVM\) startup parameter. |
|Description|String|No|LED driver|The description of the driver. The description can be a maximum of 256 bytes in length. |
|SourceConfig|String|No|\{"ossAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30c\*\*\*\*\*\*/ck3n3koe200003h6zf\*\*\*\*\*\*.zip"\}|The source of the driver code. Set this parameter to a JSON string in the following format:

 `{"ossAddress":"http://***/driver_code.zip"}` In the JSON string, `ossAddress` specifies the URL of the driver code stored in Object Storage Service \(OSS\). If you want to upload the driver code and obtain the URL of the driver code stored in OSS by using API operations, call the [CreateOssPreSignedAddress](~~155858~~) operation first. |
|DriverConfig|String|No|\[\{"format":"JSON","content":"\{\\"defaultConfig\\":\\"this is default driver config demo\\"\}"\}\]|The configuration of the driver. Set this parameter to a JSON string in the following format:

 `{"format":"JSON","content":"{}"}` The JSON string contains the following parameters:

 -   format: the format of the driver configuration. Valid values: KV \(key-value pair\), JSON \(JSON string\), and FILE \(configuration file\).
-   content: the content of the driver configuration. If you set the format parameter to KV or JSON, set this parameter to the configuration content of the driver. If you set the format parameter to FILE, set this parameter to the URL of the driver configuration file stored in OSS.

**Note:** To obtain the URL of the driver configuration file stored in OSS, call the [CreateOssPreSignedAddress](~~155858~~) operation. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the Internet of Things \(IoT\) service instance. This parameter is not required for the public instance but required for Enterprise Edition instances. |
|ConfigCheckRule|String|No|\{"deviceConfig":\{"required":false\},"driverConfig":\{"required":false\}\}|The rule for verifying configurations. Set this parameter to a JSON string in the following format:

 `{"deviceConfig":{"required":false},"driverConfig":{"required":false}` The JSON string contains the following parameters:

 -   driverConfig: the rule for verifying the configuration of the driver when the driver is to be deployed in an edge instance.
-   deviceConfig: the rule for verifying the configurations of devices that use the driver when the driver is to be deployed in an edge instance.

 `required`: A value of true indicates that the corresponding parameter is required. A value of false indicates that the corresponding parameter is optional. |
|ContainerConfig|String|No|\{"privileged":1,"devMappings":\[\],"volumeMappings":\[\],"hostNetworkMode":0,"portMappings":\[\]\}|The configuration of the container where the driver runs. Set this parameter to a JSON string. For more information about parameters in the JSON string, see the following parameter description of **ContainerConfig**. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this operation. For more information about common request parameters, see [Common parameters](~~135196~~).

**Parameter description of ContainerConfig**

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|privileged

|Integer

|No

|Specifies whether to enable the privilege mode for the container. Valid values:

 0: disables the mode.

 1: enables the mode. |
|hostNetworkMode

|Integer

|No

|Specifies whether to enable the host mode for the container. Valid values:

 0: disables the mode.

 1: enables the mode. |
|portMappings

|List

|No

|The mapping of network ports. This parameter is not required if the hostNetworkMode parameter is set to 1. You can specify a maximum of 10 mapping records in this parameter. For more information about specific parameters, see the following parameter description of portMappings. |
|devMappings

|List

|No

|The mapping of devices. This parameter is not required if the privileged parameter is set to 1. You can specify a maximum of 10 mapping records in this parameter. For more information about specific parameters, see the following parameter description of devMappings. |
|volumeMappings

|List

|No

|The mapping of volumes. You can specify a maximum of 10 mapping records in this parameter. For more information about specific parameters, see the following parameter description of volumeMappings. |

**Parameter description of portMappings**

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|hostPort

|Integer

|Yes

|The port number of the host where the container resides. Valid values: 1 to 65535. |
|containerPort

|Integer

|Yes

|The port number of the container. Valid values: 1 to 65535. |
|protocol

|Integer

|Yes

|The type of the protocol that is used for communication between the mapping ports. Valid values: tcp and udp. |

**Parameter description of devMappings**

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|hostPath

|String

|Yes

|The name of the device that the driver needs to access. The name must be 1 to 128 characters in length and start with **/dev/**. |
|permission

|String

|Yes

|The permissions that the driver has for the device. Valid values:

 ro: The driver has only the read permissions for the device.

 rw: The driver has both the read and write permissions for the device. |
|comment

|String

|No

|The remarks for the mapping. The remarks must be 1 to 128 characters in length. |

**Parameter description of volumeMappings**

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|hostPath

|String

|Yes

|The host path of the volume that the driver needs to access. The path must be 1 to 128 characters in length and cannot contain spaces. |
|containerPath

|String

|Yes

|The path for accessing the volume in the container. The path must be an absolute path that starts with a forward slash \(/\). The path must be 2 to 128 characters in length and cannot contain spaces. Do not set this parameter to the root directory. |
|permission

|String

|Yes

|The permissions that the driver has for the volume. Valid values:

 ro: The driver has only the read permissions for the volume.

 rw: The driver has both the read and write permissions for the volume. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|Success|The return code of the operation. A value of Success indicates that the call was successful. Other values indicate that specific errors occurred. For more information, see [Error codes](~~135200~~). |
|ErrorMessage|String|request parameter error|The error message that is returned if the call failed. |
|RequestId|String|001ADA35-8846-4B6F-93E7-E5C076F8BB56|The ID of the request. |
|Success|Boolean|true|Indicates whether the call was successful. A value of true indicates that the call was successful. A value of false indicates that the call failed. |

## Examples

Sample requests

```
http(s)://iot.cn-shanghai.aliyuncs.com/? Action=CreateEdgeDriverVersion
&ContainerConfig={"privileged":1,"devMappings":[],"volumeMappings":[],"hostNetworkMode":0,"portMappings":[]}
&DriverId=fec565038d7544978d9aed5c1a******
&Description=LED driver
&DriverVersion=1.2.0
&Argument=-XX:+PrintGCDetails
&SourceConfig={"ossAddress":"http://nova-scene-daily.oss-cn-shanghai.aliyuncs.com/driver/a8d6e4acc6941ecea8f0cfb30c******/ck3n3koe200003h6zfgrxxlua.zip"}
&DriverConfig=[{"format":"JSON","content":"{\"defaultConfig\":\"this is default driver config demo\"}"}]
&EdgeVersion=2.0.0
&ConfigCheckRule={"deviceConfig":{"required":false},"driverConfig":{"required":false}}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateEdgeDriverVersionResponse>
      <RequestId>001ADA35-8846-4B6F-93E7-E5C076F8BB56</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
</CreateEdgeDriverVersionResponse>
```

`JSON` format

```
{
  "RequestId": "001ADA35-8846-4B6F-93E7-E5C076F8BB56",
  "Code": "Success",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

