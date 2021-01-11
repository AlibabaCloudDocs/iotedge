---
keyword: [OTA升级, Link IoT Edge OTA升级]
---

# OTA升级

物联网平台提供OTA升级服务，您只需在控制台上传新的固件，即可将升级消息推送到设备端，完成设备在线升级。

物联网边缘计算使用[OTA升级](/cn.zh-CN/监控运维/OTA升级/推送升级包到设备端.md)时，有以下限制条件。

## 准备工作

1.  您需要在[下载地址](/cn.zh-CN/产品简介/发布历史/下载地址.md)中选择需要升级的Link IoT Edge标准版（LE Standard）软件包并下载到本地。

    例如，下载的是X86-64系统v2.0.0版本的软件包，包名为link-iot-edge-x86-64-v2.0.0.tar.gz。

    **说明：** 仅支持v2.0.0及以上版本的Link IoT Edge标准版（LE Standard）软件包使用OTA升级服务。

2.  在下载好Link IoT Edge标准版软件包的路径下，执行如下命令生成config.json文件。

    本示例中，在X86-64系统环境中link-iot-edge-x86-64-v2.0.0.tar.gz文件所在路径下执行命令。

    ```
    echo '{"ApiVersion":"1.0","Type":"LinkEdge"}' > config.json
    tar -czf upgrade-package.tar.gz config.json link-iot-edge-x86-64-v2.0.0.tar.gz
    ```

3.  将生成的upgrade-package.tar.gz文件上传到[物联网平台控制台](http://iot.console.aliyun.com/)个人实例或公共实例的**监控运维** \> **OTA升级**。


## 设备端软件包要求

-   要求/linkedge/run/binary-ota/的剩余空间不少于Link IoT Edge自包含软件包大小及解压缩后的大小之和。各版本自包含软件包大小请见[下载地址](/cn.zh-CN/产品简介/发布历史/下载地址.md)。
-   要求/linkedge/gateway/build/的剩余空间不少于自包含包解压缩后的大小。

## 控制台升级设置

-   新增固件时：

    |参数|描述|
    |:-|:-|
    |升级包版本号|必须使用v2.0.0及以上版本的Link IoT Edge，请在[下载地址](/cn.zh-CN/产品简介/发布历史/下载地址.md)中获取Link IoT Edge版本号。|
    |签名算法|仅支持**MD5**方式。|

-   验证升级包、批量升级时：

    |参数|描述|
    |:-|:-|
    |升级包类型|仅支持**整包**升级。|


