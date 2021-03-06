---
keyword: [Modbus, 官方驱动]
---

# Modbus驱动

Link IoT Edge提供Modbus官方驱动，用于支持工业领域广泛应用的Modbus通信协议设备。本文主要介绍Modbus驱动及其用法。

## 概览

Modbus是常用的应用层数据通信协议，阿里云官方Modbus驱动（以下简称Modbus驱动）支持Modbus RTU和Modbus TCP两种交互。

Modbus驱动可以直接连接Modbus从设备，示意图如下所示。

![Modbus驱动直接连接设备](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3590953951/p39309.png)

Modbus驱动也可以通过Modbus网关连接Modbus从设备，示意图如下所示。

![Modbus驱动通过网关连设备](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3590953951/p39310.png)

Modbus驱动支持的功能有读取输入状态和输入寄存器、读取和写入线圈状态、保持寄存器。

Link IoT Edge提供C和Python语言Modbus驱动，同时根据CPU架构的不同，有多种C语言Modbus驱动。您可以直接从控制台部署Modbus驱动到网关，也可以从控制台下载Modbus驱动代码进行修改，作为您的自定义驱动使用。

本文以示例方式介绍Modbus官方驱动的使用步骤，具体操作如下文所示。

## 前提条件

请确保已创建边缘实例并上线网关，具体操作请参见[环境搭建](/cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md)。

## 一、分配驱动

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)。

2.  左侧导航栏单击**边缘实例**，在已创建的边缘实例右侧单击**查看**。

3.  在**实例详情**页面设备与驱动页签下，单击**全部驱动**右侧的`+`图标 。

4.  在分配驱动面板中，选择**官方驱动**，根据网关CPU架构选择需要使用的Modbus驱动，单击对应操作栏中的**分配**。然后单击**关闭**。

    **说明：**

    -   C语言Modbus驱动，需在v1.8.4及以上版本的Link IoT Edge中使用。
    -   Python语言Modbus驱动，仅支持在Link IoT Edge专业版中使用。
    ![选驱动](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4078520061/p48381.png)


## 二、配置驱动

1.  单击已分配的Modbus驱动，在设备列表右侧单击**驱动配置**。

2.  在弹出面板中单击**添加通道**。

    通道是网关与具体物理设备之间的连接介质。

    ![添加通道](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0068420061/p48436.png)

3.  根据界面提示设置参数，然后单击**确定**。

    |参数|描述|
    |:-|:-|
    |通道名称|设置通道名称，需在网关维度具有唯一性。支持中文汉字、英文字母、数字和下划线（\_），长度不超过1~30个字符，1个中文汉字算2个字符。|
    |传输模式|支持RTU、TCP和LoRa LAN三种。 |
    |当传输模式为RTU时，需设置以下参数：|
    |串口|设置串口，如/dev/ttyUSB0、/dev/ttyUSB1。支持英文字母、数字、正斜杠（/）和下划线（\_），长度限制1~64字符。|
    |波特率|表示每秒传送的符号个数，从下拉列表中选择。|
    |数据位|表示一组数据实际包含的数据位数，从下拉列表中选择。|
    |校验位|从下拉列表中选择奇偶校验、或者无校验。|
    |停止位|用于表示单个包的最后一位，从下拉列表中选择。|
    |当传输模式为TCP时，需设置以下参数：|
    |IP地址|Modbus设备IP地址，输入点分十进制格式的地址。|
    |端口号|Modbus设备端口号，输入1~65535范围的整数。|
    |当传输模式为LoRa LAN时，需设置以下参数：|
    |DevAddr|设备地址。请填写8位十六进制数值，例如`66be****`。|
    |AppSKey|应用会话密钥。请填写32位十六进制数值，例如`623bd505f042090b5af660954509****`。|
    |NwkSKey|网络会话密钥。请填写32位十六进制数值，例如`e1336a94a03aa3beae55b737acda****`。|
    |Class|通信节点的特定类。当前仅支持C特定类，即随时接收设备上报的数据。|
    |上行 FPort|上行应用端口，取值范围为1~223。|
    |下行 FPort|下行应用端口，取值范围为1~223。|

4.  （可选）在设备列表右侧，单击**容器配置**，根据如下参数说明，对当前驱动进行容器配置。配置完成后单击**保存**。

    **说明：** 仅在产品规格为专业版的边缘实例中，允许设置**容器配置**。

    |参数|描述|
    |--|--|
    |是否使用宿主机host模式|选择是否隔离容器的网络。直接使用宿主机网络环境。     -   是：表示不隔离容器的网络，直接使用宿主机网络环境。
    -   否：表示隔离容器的网络，需要设置网络端口映射。 |
    |网络端口映射|当是否使用宿主机host模式为否时出现的参数。函数的网络环境和宿主机的环境是完全隔离的。通过网络端口映射，将容器内函数的监听端口映射到宿主机的某一个端口上，实现不同主机上的客户端程序，能够访问该函数提供的服务。最多支持映射10条网络端口。 例如，运行在宿主机容器内的`fc-http-server`函数，通过80端口对外界提供服务。此时，其它主机上的客户端程序，无法通过访问宿主机的80端口，访问到`fc-http-server`函数。因此需要将`fc-http-server`函数所在的容器端口映射到宿主机的某一个端口上（例如将容器内的80端口映射到宿主机8080端口），允许其它主机上的客户端程序通过访问`宿主机的IP地址：8080`，访问到容器内部的`fc-http-server`函数。 |
    |是否启动特权模式|容器内的root用户实际上只是宿主机的一个普通用户。若在容器内部做修改系统时间、使用mount命令等需要root权限的操作，则需要赋予容器privileged特权。

**说明：** 特权模式下，容器内部拥有宿主机的root权限，而且宿主机的所有设备会默认映射到容器内部，即无需配置设备映射。 |
    |设备映射|当是否启动特权模式为否时出现的参数。设备管理系统和宿主机的环境是完全隔离的。当一个函数需要访问宿主机的设备（例如串口）时，需要将设备映射到运行函数的容器内部。最多可添加10个设备映射。|
    |卷映射|文件系统和宿主机的环境是完全隔离的。当一个函数需要访问宿主机的文件时，需要将文件映射到运行函数的容器内部。最多可添加10个卷映射。|
    |内存限制|设置容器的内存上限。 当容器内存使用超过限制时，容器会被重启。如果内存限制值过小，可能会导致容器内的应用运行失败。默认内存为1024 MB，请根据容器内应用大小，上调内存限制。|


## 三、驱动关联子设备

1.  单击设备列表区域框下的**分配子设备**，在Modbus驱动下为边缘实例分配设备。

    您可以分配已有的Modbus设备，也可以根据下面的步骤，新建Modbus设备。

    **说明：** 分配已有的Modbus设备时，该设备所属产品必须接入网关，且接入网关协议为Modbus。详细说明请参见[创建产品](/cn.zh-CN/设备接入/创建产品.md)。

2.  在右侧弹出的分配子设备面板中，单击**添加子设备**。

    ![添加子设备按钮](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7743119951/p37903.png)

3.  在添加设备对话框，单击**新建产品**，创建Modbus设备所属产品。

    ![新增客厅灯产品](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7743119951/p37904.png)

4.  在创建产品对话框设置参数后，单击**完成**。

    ![创建产品](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8128853951/p48524.png)

    |参数|描述|
    |--|--|
    |产品名称|设置产品名称，产品名称在账号内具有唯一性。支持中文、英文字母、数字、下划线（\_）、短划线（-）、at符号（@）和英文圆括号，长度限制4~30个字符，一个中文汉字算2个字符。|
    |所属品类|选择品类，为该产品定义[物模型](/cn.zh-CN/设备管理/物模型/什么是物模型.md)。此处选择自定义品类。|
    |接入网关协议|此处必须选择Modbus。|
    |认证方式|选择适合您设备的认证方式。详情请参见[设备安全认证](/cn.zh-CN/设备接入/设备安全认证/概述.md)。|
    |产品描述|添加对该产品的描述。可以为空。|

5.  在添加设备对话框，产品自动分配已创建的产品，单击产品下的前往配置，为产品添加自定义功能。

    **说明：** 您也可以使用[Modbus调试工具](/cn.zh-CN/用户指南/设备接入/官方驱动/Modbus调试工具.md)配置Modbus产品，但需要先完成添加设备并分配到边缘实例的操作，再使用调试工具。

    ![前往设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3311407951/p48540.png)

    系统跳转到[物联网平台控制台](http://iot.console.aliyun.com/)的**产品详情**页面**功能定义**页签。单击**编辑草稿**，在弹出页面中单击**添加自定义功能**。

    ![添加功能](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9128853951/p48541.png)

6.  在**添加自定义功能**对话框，根据实际情况设置属性参数。具体操作请参见[单个添加物模型](/cn.zh-CN/设备管理/物模型/单个添加物模型.md)。

    在配置物模型属性的过程中，单击**新增扩展描述**设置如下**扩展描述**参数，将属性映射到寄存器中。官方Modbus驱动会将所有的属性聚合为Modbus数据请求，驱动收到Modbus数据之后再转换为物模型数据。

    ![扩展描述](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9128853951/p48543.png)

    参数说明如下所示，详细的参数解释请参见[单个添加物模型](/cn.zh-CN/设备管理/物模型/单个添加物模型.md)中“扩展描述”的说明。

    |名称|描述|
    |--|--|
    |操作类型|指操作Modbus的功能码。 此处选择**保持寄存器（读写，读取使用0x03，写入使用0x06）**。 |
    |寄存器地址|填写十六进制，以`0x`开头。 根据您自己设备的属性地址设置寄存器地址。例如，要调试温度属性，您设备的温度属性地址为1，则寄存器地址可设置为0x1。 |
    |原始数据类型|如采集的温度值的数据类型为浮点型。|
    |取值范围|取值范围指的是原始数据经过缩放因子处理之后的取值范围，超出取值范围的数据会被丢弃。|
    |交换寄存器内高低字节|是否把寄存器内16位数据的前后8个bits互换。此处设置为互换true。|
    |交换寄存器顺序|是否把原始数据32位数据的bits互换。此处设置为不互换false。|
    |缩放因子|指缩放系数，如采集的值为100， 但真实的值为10，因此需要缩放10倍，故缩放因子填写0.1即可。如放大10倍（即真实的值为1000），则放大因子为10。|
    |数据上报方式|有两种数据上报方式。     -   按时上报：选择按时上报后，根据步骤9中为子设备设置的数据采集间隔，采集数据并上报。
    -   变更上报：采集后的值发生变化后才会上报。 |

7.  返回实例详情页面，添加Modbus设备。

    ![Modbus产品添加设备_专有云](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9128853951/p70931.png)

8.  将新建的Modbus设备分配到边缘实例。

9.  分配设备到边缘实例后，单击设备名称对应操作栏中的**设备配置**，通过关联通道，关联设备与Modbus驱动。

    ![设备配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9128853951/p10269.png)

    |参数|描述|
    |--|--|
    |关联通道|选择[配置驱动](#section_vi5_uar_7mu)步骤2中已创建的通道。|
    |从站号|从站号是Modbus设备标识信息，在同一个通道中是唯一的。|
    |数据采集间隔|Modbus协议是半双工协议，由网关主动请求数据，因此需要指定对数据点的采集间隔时间。单位为毫秒。 **说明：** 单个属性点的采集耗时时间大概为60毫秒（ms），则采集间隔的计算方式为：

    ```
采集耗时时间(60 ms) * 该通道的所有属性点个数
    ```

例如，当前Modbus总线通道上有10个设备，且每个设备有10个属性点，即采集间隔时间应大于等于6000 ms（60 ms \* 10 \* 10 = 6000 ms），这样才能保证每个属性点能正常上报。 |


## 四、部署边缘实例

1.  （可选）在部署实例前，可以使用[Modbus调试工具](/cn.zh-CN/用户指南/设备接入/官方驱动/Modbus调试工具.md)，测试网关能否连接该Modbus设备，同时也可以测试Modbus设备所属产品的物模型是否配置正确。

2.  在实例详情页面，单击右上角**部署**，部署边缘实例。


## 常见问题

Modbus官方驱动上报消息到云端时，是按照设备维度上报，还是属性维度上报？

答：Modbus官方驱动在每个采集周期内，按照设备维度进行采集和上报数据。例如，1个Modbus设备有100个属性，数据采集间隔为5秒，那么Modbus驱动每5秒上报云端1条消息（因为是1个设备）。

