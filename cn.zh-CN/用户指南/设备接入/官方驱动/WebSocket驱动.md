---
keyword: [WebSocket, WebSocket驱动]
---

# WebSocket驱动

Link IoT Edge提供用于接入WebSocket通信协议设备的驱动。根据网关设备使用架构的不同，Link IoT Edge提供多种WebSocket驱动。您可以直接从控制台部署WebSocket驱动到网关。

使用WebSocket驱动接入设备时需要遵循Link IoT Egde的WebSocket接入协议。详情请参见[物联网边缘计算设备接入协议（WebSocket版）](https://github.com/aliyun/linkedge-thing-access-websocket_client_sdk/blob/master/protocol-design-description.md)。

WebSocket驱动可以直接接受设备的接入，示意图如下所示。

![WebSocket驱动直接设备](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0490953951/p49749.png)

WebSocket驱动也可以通过网关接受设备的接入，示意图如下所示。

![WebSocket驱动网关接设备](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1490953951/p50381.png)

本文以示例方式介绍WebSocket官方驱动的使用步骤，具体操作如下文所示。

## 前提条件

请确保已创建边缘实例并上线网关，具体操作请参见[环境搭建](/cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md)。

## 一、分配驱动

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)。

2.  左侧导航栏单击**边缘实例**，在已创建的边缘实例右侧单击**查看**。

3.  在**实例详情**页面，选择设备与驱动右侧的`+`图标。

4.  在分配驱动面板，选择**官方驱动**并根据网关CPU架构选择需要使用的WebSocket驱动，单击对应操作栏中的**分配**。然后单击**关闭**。

    **说明：** WebSocket驱动，仅支持在v2.0.0及以上版本的Link IoT Edge中使用。

    ![分配WebSocket驱动到实例](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5258420061/p49844.png)


## 二、配置驱动

1.  单击已分配的WebSocket驱动，在设备列表右侧单击**驱动配置**。

    根据界面提示设置参数，然后单击**确定**。

    ![驱动配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6997599851/p49853.png)

    |参数|描述|
    |--|--|
    |IP地址|WebSocket驱动监听地址，默认为驱动所在机器的IP地址。|
    |端口号|WebSocket驱动监听端口，范围为1 ~ 65535，默认端口为17682。|
    |是否加密|是否使用TLS加密，默认不加密。若选择**是**，需要上传公钥和私钥文件。     -   公钥文件：上传公钥证书文件，证书文件格式必须为.cer，名称不支持中文字符。
    -   私钥文件：上传私钥文件，文件格式必须为.pvk，名称不支持中文字符。 |

2.  （可选）在设备列表右侧，单击**容器配置**，根据如下参数说明，对当前驱动进行容器配置。配置完成后单击**保存**。

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

1.  单击设备列表区域框下的**分配子设备**，在WebSocket驱动下为边缘实例分配设备。

    您可以分配已有的WebSocket设备，也可以根据下面的步骤，新建WebSocket设备。

2.  在右侧弹出的分配子设备面板中，单击**添加子设备**。

    ![添加子设备按钮](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7743119951/p37903.png)

3.  在添加设备对话框，单击**新建产品**，创建WebSocket设备所属产品。

    ![新增产品](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7743119951/p37904.png)

4.  在创建产品对话框设置参数后，单击**完成**。

    ![websocket驱动产品](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6997599851/p72964.png)

    |参数|描述|
    |--|--|
    |产品名称|设置产品名称，产品名称在账号内具有唯一性。支持中文、英文字母、数字、下划线（\_）、连接号（-）、@符号和英文圆括号，长度限制4~30，一个中文汉字算2位。|
    |所属分类|选择品类，为该产品定义[物模型](/cn.zh-CN/设备管理/物模型/什么是物模型.md)。此处选择自定义品类。|
    |接入网关协议|此处必须选择自定义。|
    |认证方式|选择适合您设备的认证方式。详情请参见[设备安全认证](/cn.zh-CN/设备接入/设备安全认证/概述.md)。|
    |产品描述|添加对该产品的描述，可以为空。|

5.  在添加设备对话框，输入DeviceName，添加WebSocket设备。

6.  将新建的WebSocket设备**分配**到边缘实例。

7.  分配设备到边缘实例后，单击设备名称对应操作栏中的**设备配置**，关联设备与WebSocket驱动。

    ![设备配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7805722951/p50342.png)

    设备IP：接入设备或设备所在网关的IP。

    **说明：** 如果配置了该参数，则Link IoT Edge会严格校验IP。仅允许来自该IP地址的指定设备接入。


## 四、部署边缘实例

在实例详情页面，单击右上角**部署**，重新部署边缘实例。

