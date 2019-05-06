# 使用Modbus TCP连接Modbus从设备 {#concept_z5s_gkc_ggb .concept}

Modbus通信协议遵循主设备和从设备的通信步骤，边缘网关中Modbus驱动使用Master角色采取主动询问方式，送出Query Message给Modbus从设备，然后由Modbus从设备依据接到的Query Message内容准备Response Message回传给网关。

## 前提条件 {#section_yw1_gsd_ggb .section}

1.  准备一个Ubuntu 16.04 x86\_64系统，用于运行网关。
2.  准备一个Windows系统的机器，用于运行模拟的Modbus从设备。
3.  从[这里](https://www.modbustools.com/download.html)获取Modbus从设备模拟软件，并下载到Windows机器上。
4.  检查Windows机器的防火墙，确保能正常访问Modbus从设备502端口，若不能访问，请关闭防火墙或者防火墙中允许访问端口。

## 操作步骤 {#section_zv4_gsd_ggb .section}

1.  以阿里云账号登录[物联网控制台](http://iot.console.aliyun.com/)。
2.  参考[环境搭建](../../../../cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md#)内容，创建边缘实例，上线网关。
3.  参考[创建产品](../../../../cn.zh-CN/用户指南/产品与设备/创建产品.md#)，创建Modbus产品。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231135158_zh-CN.png)

    其中，部分参数必须按如下说明设置。

    |参数|描述|
    |--|--|
    |所属分类|选择**自定义分类**。|
    |是否接入网关|选择**是**。|
    |接入网关协议|选择**Modbus**。|

4.  参考[新增物模型](../../../../cn.zh-CN/用户指南/产品与设备/物模型/新增物模型.md#)，在产品详情页，为刚创建的Modbus产品添加物模型。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231135180_zh-CN.png)

5.  单击**扩展描述**。

    通过新增扩展描述对Modbus的点位进行描述。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231135181_zh-CN.png)

    对Modbus点位描述时需要参考模拟的Modbus从设备中的点位设置，如下图所示。本文示例产品中创建了3个属性点aaa、bbb、ccc分别对应Modbus从设备中点位地址0，1，2三个地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231135182_zh-CN.png)

6.  参考[单个创建设备](../../../../cn.zh-CN/用户指南/产品与设备/创建设备/单个创建设备.md#)，添加Modbus设备。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231135186_zh-CN.png)

7.  参考[子设备通信通道](../../../../cn.zh-CN/用户指南/设备接入/子设备通信通道.md#)，为网关添加Modbus通道。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231435187_zh-CN.png)

8.  配置并部署边缘实例。
    1.  将已创建的Modbus设备分配到边缘实例中，作为网关的子设备后，为该子设备配置Modbus官方驱动，关联子设备通信通道。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231446392_zh-CN.png)

    2.  配置如下图消息路由。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231435188_zh-CN.png)

    3.  部署边缘实例。
9.  在**设备管理** \> **设备**页，运行状态页签中，查看设备显示的属性。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/155713231435189_zh-CN.png)


