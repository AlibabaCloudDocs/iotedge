# LinkDriver驱动

对于集成了阿里云设备接入Link SDK的设备，物联网边缘计算提供LinkDriver驱动，将此类设备连接到Link IoT Edge实现与云端通信。

LinkDriver驱动示意图如下所示。

![linkkit设备驱动示意图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2311407951/p81752.png)

## 前提条件

-   已下载并集成Link SDK到您的设备。具体操作，请参见[设备接入Link SDK文档]()。
-   已创建边缘实例并上线网关。具体操作，请参见[环境搭建](/cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md)。

## 一、修改Link SDK

使用LinkDriver驱动之前，需要修改设备上的Link SDK内容，使设备能够连接到Link IoT Edge所在的网关。

本文以最新版C语言Link SDK 4.x版本为例，说明修改方法。其它语言Link SDK，请参考C语言SDK说明修改。

1.  打开C语言Link SDK的demos/mqtt\_basic\_demo.c文件。

2.  按照如下图红框所示的说明，修改接入MQTT的参数值。

    **说明：** 其中，将IP地址`192.168.56.102`替换为您自己的网关IP地址，其余参数设置与图片内容保持一致。

    ![linkkit接入mqtt信息1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0205489061/p81754.png)

3.  保存修改的内容，然后重新编译Link SDK并更新到设备上。详细操作，请参见[Link SDK文档]()。


## 二、分配驱动

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)。

2.  左侧导航栏单击**边缘实例**，在已创建的边缘实例右侧单击**查看**。

3.  在**实例详情**页面设备与驱动页签下，单击**全部驱动**右侧的`+`图标 。

4.  在分配驱动面板中，选择**官方驱动**，在LinkDriver驱动右侧单击**分配**。然后单击**完成**。

    ![分配LinkDriver驱动](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8923420061/p127026.png)


## 三、驱动关联子设备

1.  单击已分配的LinkDriver驱动，在设备列表区域中单击**分配子设备**。

2.  在右侧弹出的分配子设备面板中，单击**添加子设备**。

    ![添加子设备按钮](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7743119951/p37903.png)

3.  在添加设备对话框，单击**新建产品**，创建Link SDK设备所属产品。

    ![新增客厅灯产品](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7743119951/p37904.png)

4.  在创建产品对话框设置参数后，单击**完成**。

    |参数|描述|
    |--|--|
    |产品名称|设置产品名称，产品名称在账号内具有唯一性。支持中文、英文字母、数字、下划线（\_）、短划线（-）、at符号（@）和英文圆括号，长度限制4~30个字符，一个汉字算2个字符。|
    |所属品类|选择品类，为该产品定义[物模型](/cn.zh-CN/设备管理/物模型/什么是物模型.md)。此处选择自定义品类。|
    |接入网关协议|此处选择自定义。|
    |认证方式|选择适合您设备的认证方式。详情请参见[设备安全认证](/cn.zh-CN/设备接入/设备安全认证/概述.md)。|
    |产品描述|添加对该产品的描述。可以为空。|

5.  在添加设备对话框，产品自动分配已创建的产品，单击产品下的前往配置，为产品添加自定义功能。

    ![前往设置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3311407951/p48540.png)

    系统跳转到[物联网平台控制台](http://iot.console.aliyun.com/)的**产品详情**页面**功能定义**页签。单击**编辑草稿**，在弹出页面的**默认模块**中单击**添加自定义功能**。

6.  在**添加自定义功能**对话框，根据实际情况设置属性参数。具体操作，请参见[单个添加物模型](/cn.zh-CN/设备管理/物模型/单个添加物模型.md)。

7.  返回实例详情页面，添加Link SDK设备。

    ![添加Link SDK设备](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3311407951/p127032.png)

8.  将新建的Link SDK设备分配到边缘实例。


## 四、部署边缘实例

1.  在实例详情页面，右上角单击**部署**，部署边缘实例。部署成功后边缘实例名称后显示**部署成功**。

2.  查看设备运行状态。

    实例部署成功后，可以查看设备连接状态和运行状态。这些信息可以在阿里云物联网平台（云端）查看，也可以在边缘网关运行环境中的驱动运行日志中查看。

    1.  在实例详情页面设备与驱动页签，单击LinkDriver驱动，查看设备连接状态。

        ![LinkSDK设备连接状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3311407951/p127034.png)

    2.  单击设备名称右侧操作栏中的**查看**，跳转到物联网平台设备详情页面。

    3.  单击**物模型数据**页签下的**运行状态**，查看设备上报的数据。

3.  查看驱动运行数据和日志。

    1.  登录Link IoT Edge所在网关。

    2.  进入LinkDriver驱动文件所在目录，查看驱动日志。

        ```
        cd /linkedge/run/logger/fc-base/LinkDriver 
        ```


