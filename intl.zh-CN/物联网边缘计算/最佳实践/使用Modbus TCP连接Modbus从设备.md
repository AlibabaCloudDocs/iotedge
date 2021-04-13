---
keyword: [Modbus TCP, 连接Modbus从设备, Modbus]
---

# 使用Modbus TCP连接Modbus从设备

Modbus通信协议遵循主设备和从设备的通信步骤，边缘网关中Modbus驱动使用Master角色（主设备），采取主动询问方式，发送Query Message给Modbus从设备，然后由Modbus从设备依据接到的Query Message内容准备Response Message回传给网关。

## 准备工作

1.  准备一个Ubuntu 16.04 x86\_64系统，用于运行网关。

2.  准备一个Windows系统的机器，用于运行模拟的Modbus从设备。

3.  从[Modbus工具下载地址](https://www.modbustools.com/download.html)中获取Modbus从设备模拟软件，下载并安装到Windows机器上。

4.  检查Windows机器的防火墙，确保能正常访问Modbus从设备502端口，若不能访问，请关闭防火墙或者防火墙中允许访问端口。

5.  创建边缘实例并上线网关，具体操作请参见[环境搭建](/intl.zh-CN/物联网边缘计算/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md)。


## 一、分配Modbus驱动到边缘实例

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)。

2.  在左侧导航栏，选择**边缘实例**，单击目标边缘实例右侧的**查看**。

3.  根据网关CPU，分配合适的官方Modbus驱动到边缘实例，具体操作请参见[Modbus驱动](/intl.zh-CN/物联网边缘计算/用户指南/设备接入/官方驱动/Modbus驱动.md)中的分配驱动步骤。

    ![选驱动](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4078520061/p48381.png)

4.  单击已分配的Modbus驱动，在设备列表右侧单击**驱动配置**。

5.  在弹出页面中单击**添加通道**，为Modbus驱动添加通道。

    参数说明请参见[Modbus驱动-驱动配置](/intl.zh-CN/物联网边缘计算/用户指南/设备接入/官方驱动/Modbus驱动.md)。

    ![添加modbus通道](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2780690161/p35187.png)


## 二、Modbus驱动关联子设备

1.  单击设备列表区域框下的**分配子设备**，在Modbus驱动下为边缘实例分配设备。

    您可以分配已有的Modbus设备，也可以根据下面的步骤，新建Modbus设备。

    **说明：** 分配已有的Modbus设备时，该设备所属产品必须接入网关，且接入网关协议为Modbus。详细说明请参见[创建产品](/intl.zh-CN/设备接入/创建产品.md)。

2.  在右侧弹出的分配子设备面板中，单击**添加子设备**。

    ![添加子设备按钮](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7743119951/p37903.png)

3.  在添加设备对话框，单击**新建产品**，创建Modbus设备所属产品。

    ![新增客厅灯产品](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7743119951/p37904.png)

4.  在创建产品对话框设置参数后，单击**完成**。

    |参数|描述|
    |--|--|
    |产品名称|设置产品名称，产品名称在账号内具有唯一性。支持中文、英文字母、数字、下划线（\_）、短划线（-）、at符号（@）和英文圆括号，长度限制4~30个字符，一个中文汉字算2个字符。|
    |接入网关协议|此处必须选择Modbus。|
    |认证方式|选择适合您设备的认证方式。详情请参见[设备安全认证](/intl.zh-CN/设备接入/设备安全认证/概述.md)。|
    |产品描述|添加对该产品的描述。可以为空。|

5.  在添加设备对话框，产品自动分配已创建的产品，单击产品下的前往配置，为产品添加自定义功能，具体操作请参见[单个添加物模型](/intl.zh-CN/设备管理/物模型/单个添加物模型.md)。

    ![modbus产品添加自定义功能](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4611989851/p63920.png)

6.  在添加自定义功能对话框，设置属性参数后单击**新增扩展描述**，设置如下扩展描述。

    通过新增扩展描述，对Modbus设备的点位进行描述。

    ![扩展描述](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5611989851/p35181.png)

    其中，设置Modbus设备的寄存器地址时，需要参考模拟的Modbus从设备中的点位设置，如下图所示。本文示例产品中创建了3个属性点aaa、bbb、ccc分别对应Modbus从设备中点位地址0、1、2三个地址。

    ![模拟设备点位](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5611989851/p35182.png)

7.  返回[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)实例详情页面**添加设备**对话框，添加Modbus设备。

    ![Modbus产品添加设备_专有云](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9128853951/p70931.png)


## 三、配置并部署边缘实例

1.  将新建的Modbus设备分配到边缘实例。

2.  分配设备到边缘实例后，单击设备名称对应操作栏中的**设备配置**，通过关联通道，关联设备与Modbus驱动。

    ![设备配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5611989851/p49270.png)

    |参数|描述|
    |--|--|
    |关联通道|选择本文上方[一、分配Modbus驱动到边缘实例](#section_3o0_ngn_roq)中已创建的通道。|
    |从站号|从站号请参见本文上方[二、Modbus驱动关联子设备](#section_vp0_c2k_2sy)中第6步Modbus从设备的ID值，即本示例中从站号为1。|

3.  在实例详情页面，单击右上角**部署**，部署边缘实例。

4.  登录[物联网平台控制台](http://iot.console.aliyun.com/)，在左侧导航栏单击**设备管理** \> **设备**，找到目标Modbus产品，单击**查看**。

    在设备详情页面单击**物模型数据** \> **运行状态**页签，查看设备显示的属性。

    ![运行状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6611989851/p35189.png)


