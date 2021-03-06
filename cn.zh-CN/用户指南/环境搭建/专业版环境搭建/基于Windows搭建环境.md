---
keyword: [环境搭建, 专业版, Windows]
---

# 基于Windows搭建环境

本文介绍如何在Windows7和Windows10的系统中搭建Link IoT Edge专业版（LE Pro）的Docker运行环境，实现网关与云端连接的步骤。

专业版（LE Pro）规格的详细说明请参见[产品规格](/cn.zh-CN/产品简介/产品规格.md)。

## 准备工作

-   LE Pro版需要您提前安装好Docker环境，Windows7系统请参见[Install Docker Toolbox on Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)，Windows10系统请参见[Install Docker for Windows](https://docs.docker.com/docker-for-windows/install/)。要求Docker版本大于v17.03。
-   在您的Windows 7或Windows 10系统机器上安装最新版本的Git bash。安装包以及安装操作请参见[官方文档](https://gitforwindows.org/)。

## 约束条件

-   目前仅支持在Windows 7和Windows 10系统中搭建专业版运行环境。
-   LE Pro版需要bash的运行环境，用于运行Link IoT Edge的脚本工具，请务必安装好Git bash。

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

2.  根据环境设置软件安装相关参数，然后单击**生成安装命令**。

    ![下载命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4249922951/p45194.png)

    |参数|描述|
    |--|--|
    |边缘网关CPU架构|您的设备系统对应的CPU架构。此处选择x86-64。|
    |产品规格|在创建边缘实例时，已选择实例中使用的Link IoT Edge版本。此处不可操作。|
    |边缘版本|选择Link IoT Edge的[发布版本](/cn.zh-CN/产品简介/发布历史/专业版.md)。 |
    |操作系统|选择您的设备对应的操作系统。此处选择Windows。|

3.  复制软件包下载命令备用。

    ![复制命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4249922951/p45201.png)

4.  登录您的Windows7或Windows10系统的机器。

5.  在git bash运行环境任意目录下执行步骤3中已复制的命令。

    ![gitbash中执行LE安装命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4249922951/p85644.png)

    该命令实现一键下载、配置并启动Link IoT Edge。命令执行完成后，会在当前目录中下载link-iot-edge.sh脚本。

    -   如果您第一次启动网关，则需要完成如下交互式配置，您可以直接按**Enter**键使用默认配置。

        -   确认启动版本。
        -   确认函数计算的runtime，函数默认运行在独立的进程中。
        -   确认是否启动流式计算，默认开启流式计算。
        -   确认是否卸载之前已安装的版本，默认卸载。
        拉取Docker镜像完成并启动可能需要等待5~10分钟，启动完成后通过docker ps命令查看相关Docker容器是否已启动，若系统显示如下图所示信息，表示启动成功。

        ![查看执行结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4249922951/p37204.png)

    -   如果不是第一次安装启动Link IoT Edge，可使用已下载的link-iot-edge.sh脚本，对Link IoT Edge进行重启、停止、获取状态、修改配置参数等操作，命令详情请见下图。

        ![Link IoT Edge其他操作](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5249922951/p44849.png)

6.  返回[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)，在左侧导航栏选择**边缘实例**，找到已创建好的边缘实例，单击右侧操作栏中的**查看**，进入**实例详情**页面，选择**网关**查看网关状态。

    打开**远程访问**按钮，可对网关进行远程管理，详细操作步骤，请参见[远程服务访问](/cn.zh-CN/用户指南/远程运维管理/远程服务访问.md)。

    ![网关在线](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0940277951/p37203.png)

7.  （可选）在实例详情页面，查看CPU使用率、内存使用率、存储使用率以及实例进程需要授权访问阿里云云监控（CloudMonitor）服务。

    1.  添加角色或分配已有的角色，并确保该角色拥有**管理云监控（CloudMonitor）的权限**。详细操作，请参见[云资源访问](/cn.zh-CN/用户指南/云资源访问.md)。

    2.  选择**监控信息**页签，打开页面右侧的**云监控状态**开关，如下图所示。

        ![国际站中文-云监控按钮](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0940277951/p101806.png)

        云监控状态打开后，可在**监控信息**页签，查看网关的各类监控信息。

8.  （可选）在实例详情页面单击**网关**页签，打开**远程访问**开关后，可对网关进行远程管理，详细操作步骤，请参见[远程服务访问](/cn.zh-CN/用户指南/远程运维管理/远程服务访问.md)。

9.  （可选）Link IoT Edge支持将边缘实例授权给其他阿里云账号操作。

    在边缘实例页面，单击左上角**授权**，在弹出对话框中单击**新增授权**，根据界面提示设置参数。

    ![实例授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2597528951/p66515.png)

    |参数|描述|
    |--|--|
    |授权用户UID|获取被授权用户的阿里云账号ID，填入此处。|
    |授权实例|选择允许该阿里云账号ID的用户进行远程运维操作的边缘实例。|


## Link IoT Edge的其它操作

-   重新配置Link IoT Edge。

    使用如下命令，对当前已安装的Link IoT Edge版本配置进行修改。

    ```
    ./link-iot-edge.sh --reconfig {Version}
    ```

    其中，\{Version\}替换为目标版本号，例如目标版本号为V1.8.2，则实际命令为`./link-iot-edge.sh --reconfig v1.8.2`。

-   停止Link IoT Edge。

    使用如下命令，可以停止所有Link IoT Edge运行的容器，但是不会删除。

    ```
    ./link-iot-edge.sh --stop
    ```

-   重新启动Link IoT Edge。

    在容器已存在且没有运行的状态下，执行如下命令可重新启动Link IoT Edge。

    ```
    ./link-iot-edge.sh --restart {Version}
    ```

    其中，\{Version\}替换为目标版本号，例如目标版本号为V1.8.2，则实际命令为`./link-iot-edge.sh --restart v1.8.2`。

-   清理Link IoT Edge。

    执行如下命令，可停止当前运行的Link IoT Edge相关容器 ，并会删除所有已安装的相关镜像，删除相关数据卷以及启动配置文件。

    ```
    ./link-iot-edge.sh --clean
    ```

-   提取Link IoT Edge的日志。

    执行如下命令，可打包Link IoT Edge的所有日志，并拷贝到当前目录。

    ```
    ./link-iot-edge.sh --packagelog
    ```


## 下一步

环境搭建完成后，您可以根据[设备接入](/cn.zh-CN/用户指南/设备接入/设备接入简介.md)内容，把您的设备接入到物联网边缘计算。同时也可以为边缘实例分配其他资源（如函数计算、消息路由等）管理您的设备。

接入设备或分配其他资源到边缘实例后，需要根据如下步骤部署边缘实例。

1.  在实例详情页面，单击右上角**部署**后，在弹出对话框中单击**确定**，部署边缘实例。

2.  当部署状态显示为**部署成功**，表示部署实例完成。您可以单击**查看日志**，查看部署详情。您也可以通过单击实例详情页面右上角的**查看部署日志**，查看历史部署情况。

    ![查看部署日志](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5359320061/p46924.png)


