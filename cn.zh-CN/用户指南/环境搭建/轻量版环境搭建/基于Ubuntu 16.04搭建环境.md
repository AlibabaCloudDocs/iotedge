---
keyword: [轻量版搭建环境, Ubuntu 16.04搭建环境]
---

# 基于Ubuntu 16.04搭建环境

本文介绍基于Ubuntu 16.04系统搭建Link IoT Edge轻量版本（LE Lite）运行环境的方法。

-   Link IoT Edge的远程登录功能依赖设备的SSH服务，请确保设备上已经开启了SSH服务。SSH的详细信息可参考[OpenSSH的使用](https://help.ubuntu.com/lts/serverguide/openssh-server.html.en?spm=a2c4g.11186623.2.11.3ce2427aDPqjvW&file=openssh-server.html.en)。
-   请确保设备的本地环回端口已启用，即在设备上执行ping 127.0.0.1命令时，返回结果正常。

    ![ping](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p72898.png)


## 创建边缘实例和网关

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)。

2.  在左侧导航栏单击**边缘实例**。

3.  创建一个边缘实例。

    1.  单击**新增实例**，在弹出对话框中设置实例名称。

        **说明：** 实例名称支持中文、英文字母大小写、数字、下划线（\_）和短划线（-），长度不超过20个字符，1个汉字算2个字符。

    2.  根据所搭建的环境，选择对应的Link IoT Edge产品规格。详细介绍，请参见[产品规格](/cn.zh-CN/产品简介/产品规格.md)。

        物联网边缘计算支持自动分配网关到边缘实例，您可以无需设置其它新增实例相关参数，直接跳转到[步骤4](#d7e274)。物联网边缘计算自动为您的边缘实例创建名为LEGatewayAuto的网关产品，并在该产品下添加一个随机命名的网关设备。

        **说明：**

        -   物联网边缘计算自动为您创建LEGatewayAuto产品时，若您已有该名称的产品，则会在该名称后添加随机后缀，作为自动创建的网关产品。
        -   物联网边缘计算已为您自动创建过一次LEGatewayAuto产品后，在您后续新建边缘实例并自动分配网关时，会在LEGatewayAuto产品下新增网关设备，分配到您新的边缘实例中。
    3.  （可选）单击**标签信息**下的**新增标签**，可以设置实例标签。通过标签您可以更加有效地归类及识别实例。您也可以不设置标签。

        若设置实例标签，请填写标签key和标签value。

        |参数|描述|
        |--|--|
        |标签key|不可为空，仅支持英文字母大小写，长度不超过20个字符，同一个边缘实例不可以重复定义标签key。|
        |标签value|不可为空，支持中文、英文字母大小写、数字、下划线（\_）和短划线（-），长度不超过20个字符，1个中文汉字算2个字符。|

4.  （可选）若您想要手动创建网关产品和设备并分配到边缘实例，请按如下步骤操作。

    1.  在**新增实例**对话框，单击**高级选项**。

    2.  在**网关产品**下单击**新建网关产品**，为实例创建网关。

        物联网边缘计算中的网关承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![创建网关产品](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p37158.png)

    3.  在**创建产品**对话框中，设置网关产品参数，然后单击**完成**。

        物联网边缘计算中的**新建网关产品**，继承了物联网平台**设备管理** \> **产品**中的产品功能，此处已自动为您简化了创建产品的步骤，以便您更快速地创建适合物联网边缘计算中使用的网关产品。

        ![创建产品](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p37159.png)

        |参数|说明|
        |--|--|
        |产品名称|为网关产品设置名称，用于后续的查询及识别网关产品。支持中文、英文字母大小写、数字和下划线（\_），长度限制4~30个字符，一个中文汉字算2位。|
        |所属品类|选择品类，为该产品定义[物模型](/cn.zh-CN/设备管理/物模型/什么是物模型.md)。

可选择的值为：

        -   **标准品类**：选择任一物联网平台预定义的品类，快速完成产品的功能定义。选择产品模板后，您可以在该模板基础上，编辑、修改、新增功能。
        -   **自定义品类**：需根据实际需要，定义产品功能。
若您需要的网关没有特殊功能定义，建议您选择**自定义品类**。 |
        |产品描述|可输入文字，用来描述产品信息。字数限制为100个字符。可以为空。|

        产品创建成功后，自动跳转回新增实例对话框，并且在**网关产品**参数下自动分配刚刚创建的网关产品。

    4.  在新增实例对话框，单击**网关设备**下的**新建网关设备**，为网关产品添加设备。

        物联网边缘计算中的新建网关设备功能，继承物联网平台**设备管理** \> **设备**的功能。

        ![新建网关设备](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p37160.png)

    5.  根据界面提示设置参数后，单击**确认**。

        |参数|描述|
        |--|--|
        |产品|系统已自动关联上一步创建的网关产品。|
        |设备名称|为该网关设备命名。设备名称需保持产品内唯一。如不填写，系统将自动生成。 **说明：** 设备名称长度为4~32个字符，可包含英文字母、数字和特殊字符，包括短划线（-）、下划线（\_）、at（@）、英文句号（.）和英文冒号（:）。 |

5.  实例参数设置完成后，单击**确定**，至此您已创建边缘实例和网关。


## 安装并启动Link IoT Edge

根据本文上方**创建边缘实例和网关**内容，创建完成边缘实例并分配网关后，您需要在网关上安装并启动Link IoT Edge。

1.  在**边缘实例**页面，单击实例名称右侧的**软件安装**。

    ![下载命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p44201.png)

2.  根据环境设置下载参数，然后单击**生成安装命令**。

    ![下载命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p44238.png)

    |参数|描述|
    |--|--|
    |边缘网关CPU架构|您的设备系统对应的CPU架构。此处选择x86-64。|
    |产品规格|在创建边缘实例时，已选择实例中使用的Link IoT Edge版本。此处不可操作。|
    |边缘版本|选择Link IoT Edge的[发布版本](/cn.zh-CN/产品简介/发布历史/轻量版.md)。 |
    |操作系统|选择您的设备对应的操作系统。此处选择Linux|

3.  复制操作系统命令备用。

    ![复制命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p44857.png)

4.  登录您Ubuntu 16.04系统的机器。

5.  任意目录下执行步骤3中已复制的命令。

    该命令实现一键下载、配置并启动Link IoT Edge。命令执行完成后，会在当前目录中下载link-iot-edge-lite.sh脚本。

    **说明：** 如果不是第一次安装启动Link IoT Edge，可使用已下载的link-iot-edge-lite.sh脚本，对Link IoT Edge进行重启、停止、获取状态、修改配置参数等操作，命令详情请见下图：

    ![轻量版操作命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1597528951/p44855.png)

    若系统显示如下信息，表示Link IoT Edge核心服务启动成功。

    ![LE启动成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2597528951/p37295.png)

    您也可以在[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)，左侧导航栏选择**边缘实例**，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，选择**网关**，查看网关状态。

    ![网关在线](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2597528951/p48694.png)

6.  （可选）Link IoT Edge支持将边缘实例授权给其他阿里云账号操作。

    在边缘实例页面，单击左上角**授权**，在弹出对话框中单击**新增授权**，根据界面提示设置参数。

    ![实例授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2597528951/p66515.png)

    |参数|描述|
    |--|--|
    |授权用户UID|获取被授权用户的阿里云账号ID，填入此处。|
    |授权实例|选择允许该阿里云账号ID的用户进行远程运维操作的边缘实例。|


## 使用systemd管理Link IoT Edge

-   配置开机自启动功能。

    ```
    wget http://remote-access-oxs.oss-cn-shanghai.aliyuncs.com/%E8%84%9A%E6%9C%AC/LinkIoTEdgeLite.service
    sudo cp LinkIoTEdgeLite.service /etc/systemd/system/LinkIoTEdgeLite.service
    sudo systemctl enable LinkIoTEdgeLite.service
    ```

-   启动Link IoT Edge。

    ```
    sudo systemctl start LinkIoTEdgeLite.service
    ```

-   重启Link IoT Edge。

    ```
    sudo systemctl restart LinkIoTEdgeLite.service
    ```

-   停止Link IoT Edge。

    ```
    sudo systemctl stop LinkIoTEdgeLite.service
    ```

-   禁用开机自启动。

    ```
    sudo systemctl disable LinkIoTEdgeLite.service
    ```


## 下一步

1.  **实例详情**页面选择**设置**页签，并在实例信息下，打开远程访问后的按钮。

2.  **实例详情**页面选择**网关**页签，在网关名称右侧的操作栏中单击**远程SSH终端**、**更多远程服务**或者**分享远程SSH终端**，远程控制网关设备、分享远程控制权限或对网关设备上的文件进行管理。详细说明请参见[远程服务访问](/cn.zh-CN/用户指南/远程运维管理/远程服务访问.md)。


