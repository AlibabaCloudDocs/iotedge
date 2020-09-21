# OPC UA设备接入实践

本文介绍基于OPC UA协议的设备（以下统称设备）接入网关，并与物联网平台交互的方法。

-   仅支持使用Link IoT Edge专业版（LE Pro），实现OPC UA设备接入。
-   根据您的实际环境，参考[专业版环境搭建](/cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md)完成边缘实例的创建，上线网关。

## 一、搭建OPC UA Server

OPC UA Server的环境依赖如下表格所示：

|依赖组件|版本要求|安装命令|
|:---|:---|:---|
|python|≥ 3.5.2|无|
|pip|≥ 9.0.1|无|
|opcua|≥ 0.98.3|pip install opcua==0.98.3|

根据以下步骤，完成OPC UA Server的搭建。该OPC UA Server模拟一个LED灯设备，该设备具有温度（temperature）属性，高温报警（high\_temperature）事件。

1.  下载OPC UA Server。

    ```
    wget http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/opcua_simulation_server.tar.gz
    ```

2.  启动OPC UA Server。

    ```
    tar -zxvf opcua_simulation_server.tar.gz
    cd opcua_simulation_server && ./opcua_simulation_server.sh
    ```


## 二、安装OPC UA客户端

使用OPC UA驱动接入OPC UA设备时需要完成设备配置操作，该操作需要借助OPC UA客户端作为辅助工具，获取OPC UA Server模拟设备信息，用于在控制台创建产品和[配置驱动](/cn.zh-CN/用户指南/设备接入/驱动开发/概览.md)时使用。

本示例使用OPC UA客户端UaExpert工具。

1.  [下载](https://www.unified-automation.com/products/development-tools/uaexpert.html)并安装OPC UA客户端UaExpert工具。

2.  安装完成后打开UaExpert工具。

    ![UaExpert工具](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6727434951/p41036.png)

3.  在工具栏中单击“`+`”图标，新增OPC UA Server。

    ![新增OPC UA Server](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6727434951/p41037.png)

4.  填写OPC UA Server的URL地址，建立与OPC UA Server的连接。URL为`OPC UA Server所在主机的IP地址:端口号`。

    **说明：** OPC UA Server示例中默认监听端口为`4840`，因此OPC UA Server的URL地址格式示例如下：

    ```
    opc.tcp://192.168.1.1:4840
    ```

    ![填写OPC UA Server的URL地址](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41038.png)

5.  配置完成URL地址后单击**OK**，显示设备信息。

    ![设备信息显示](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41040.png)


## 三、创建基于OPC UA协议的设备

1.  参考[创建产品](/cn.zh-CN/设备接入/创建产品.md)，创建OPC UA产品。

    ![新建产品](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41049.png)

    其中，部分参数设置如下：

    |参数|描述|
    |--|--|
    |所属品类|选择**标准品类**下的**边缘计算** \> **其他设备**。|
    |节点类型|选择**网关子设备**。|
    |接入网关协议|选择**OPC UA**。|

2.  参考[单个添加物模型](/cn.zh-CN/设备管理/物模型/单个添加物模型.md)，在产品详情页，为OPC UA产品添加自定义功能。

    -   添加属性
        1.  根据下图所示，设置属性参数。

            ![设置属性](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41068.png)

        2.  设置参数完成后，单击**新增扩展描述**，配置节点名称。

            ![设置扩展参数](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41069.png)

            节点名称：设备在OPC UA Server中的变量节点DisplayName的值。

            ![OPC UA Server中的变量](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p44726.png)

    -   添加服务
        1.  根据下图所示，设置服务参数。

            ![设置服务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41070.png)

        2.  单击输入参数下的**增加参数**，为产品服务新增参数。

            ![新增服务扩展参数](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41071.png)

        3.  设置参数完成后，单击**新增扩展描述**，配置节点名称。

            ![扩展描述](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p41072.png)

            节点名称：设备method在OPC UA Server中的变量节点DisplayName的值。

            ![OPC UA Server中的变量](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7727434951/p44729.png)

    -   添加事件
        1.  根据下图所示，设置事件参数。

            ![设置事件](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41073.png)

        2.  单击输出参数下的**增加参数**，为产品事件新增参数。

            ![新增服务扩展参数](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41071.png)

        3.  设置参数完成后，单击**新增扩展描述**，配置节点名称。

            ![新增事件扩展描述](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41075.png)

            节点名称：设备事件在OPC UA Server中的变量节点DisplayName的值。

            ![OPC UA Server中的变量](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p44731.png)

3.  参考[单个创建设备](/cn.zh-CN/设备接入/创建设备/单个创建设备.md)，添加设备。

    ![添加设备](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41076.png)


## 四、配置边缘实例

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)，左侧导航栏单击边缘实例。

2.  在边缘实例页面找到**前提条件**中已创建的边缘实例，单击实例名称后的**查看**。

3.  分配OPC UA驱动到边缘实例中。

    ![分配OPC UA驱动到边缘实例](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9736520061/p48705.png)

4.  选择**OPCUA**驱动，单击设备列表后的**驱动配置**，在弹出对话框中单击**添加通道**，设置通道参数。

    ![驱动配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9736520061/p41213.png)

    |参数|描述|配置举例|
    |--|--|----|
    |通道名称|OPC UA通道名称|opcua\_server|
    |通道地址|OPC UA Server的URL地址|opc.tcp://192.168.1.1:4840|
    |用户名|OPC UA Server连接用户名|demo|
    |密码|OPC UA Server连接密码|abc123|
    |方法调用超时时间|请求调用OPC UA Server调用超时时间|10|

5.  单击**分配子设备**，在**OPCUA**驱动下为边缘实例分配子设备。

    ![分配子设备](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41204.png)

6.  分配子设备成功后，单击设备名称右侧的**设备配置**。

    ![设备配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41214.png)

    |参数|描述|
    |--|--|
    |关联通道|选择已添加的通道。|
    |节点路径|设备在OPC UA Server中，从Objects开始到设备节点的绝对路径。 例如demo\_led设备在OPC UA Server中的路径为Objects/demo\_led。 |

7.  在实例详情页面右上角单击**部署**，部署边缘实例。

8.  在实例详情页面设备驱动配置页签中，选择**OPCUA**驱动，查看设备是否在线。

    ![设备在线](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8727434951/p41217.png)


