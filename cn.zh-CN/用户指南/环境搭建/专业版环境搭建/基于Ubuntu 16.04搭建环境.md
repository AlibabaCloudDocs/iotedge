# 基于Ubuntu 16.04搭建环境 {#concept_b45_2nn_lgb .concept}

本文介绍如何在Ubuntu 16.04的系统中搭建专业版（LE Pro）的Docker运行环境，实现网关与云端连接的步骤。

专业版（LE Pro）规格的详细说明请参见[产品规格](../cn.zh-CN/产品简介/产品规格.md#)。

## 准备工作 {#section_n5h_vfq_kgb .section}

LE Pro版需要您提前安装好Docker环境，请参考[Docker官方文档](https://docs.docker.com/install/linux/docker-ce/ubuntu/)安装使用您Ubuntu 16.04系统的Docker客户端。要求Docker版本大于v17.03。

## 创建边缘实例和网关 {#section_ajw_mcm_lgb .section}

1.  [物联网平台控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**。
2.  创建一个边缘实例。
    1.  单击**新增实例**，在弹出窗口中设置**实例名称**。
    2.  在**网关产品**后单击**新建网关产品**，为实例创建网关。

        物联网边缘计算中的网关，承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/155505041537158_zh-CN.png)

    3.  在新建产品页面中，设置网关产品参数，然后单击**完成**。

        物联网边缘计算中的新建网关产品功能继承物联网平台 **设备管理** \> **产品**中，高级版产品的功能。已自动为您简化创建适合物联网边缘计算中使用的网关产品步骤。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/155505041537159_zh-CN.png)

        参数说明如下：

        |参数|说明|
        |--|--|
        |产品名称|为网关产品设置名称，用于后续的查询及识别网关产品。支持中文、英文字母、数字和下划线，长度限制4~30，一个中文汉字算2位。|
        |所属分类|选择品类，为该产品定义[物模型](../cn.zh-CN/用户指南/产品与设备/物模型/概述.md#)。 可选择为：

         -   **自定义品类**：需根据实际需要，定义产品功能。
        -   任一既有功能模板。

选择任一物联网平台预定义的品类，快速完成产品的功能定义。选择产品模板后，您可以在该模板基础上，编辑、修改、新增功能。

 若您需要的网关没有特殊功能定义，建议您选择**自定义品类**。

 |
        |产品描述|可输入文字，用来描述产品信息。字数限制为100。可以为空。|

        产品创建成功后，页面自动跳转回新增实例页面，并且**网关产品**参数下自动分配了刚创建的网关产品。

    4.  在新增实例页面，单击**网关设备**后的**新建网关设备**为网关产品添加设备。

        物联网边缘计算中的新建网关设备功能继承物联网平台 **设备管理** \> **设备**的功能。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/155505041537160_zh-CN.png)

    5.  根据界面提示设置参数后，单击**确认**。

        参数说明如下：

        |参数|描述|
        |--|--|
        |产品|系统已自动关联上一步创建的网关产品。|
        |设备名称|为该网关设备命名。设备名称需保持产品内唯一。如不填写，系统将自动生成。 **说明：** 设备名称支持大写字母\[A-Z\]、小写字母\[a-z\]、数字\[0-9\]和下划线（\_）。且不能以下划线开头或结尾。

 |

    6.  （可选）在新增实例页面，单击**新增标签**，可以设置实例标签。通过标签您可以更加有效地归类及识别实例。您也可以不设置标签。
3.  实例参数设置完成后，单击**确定**，至此您已创建边缘实例和网关。

## 启动Link IoT Edge {#section_mrp_xwq_kgb .section}

1.  在左侧导航栏中选择**边缘计算** \> **边缘实例**，单击实例名称右侧的**下载**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/155505041544201_zh-CN.png)

2.  根据环境设置下载参数，然后单击**生成命令**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103158/155505041544211_zh-CN.png)

    |参数|描述|
    |--|--|
    |CPU架构|您的设备系统对应的CPU架构。此处选择x86-64。|
    |产品规格|选择Link IoT Edge的[产品规格](../cn.zh-CN/产品简介/产品规格.md#)，Link IoT Edge有专业版、标准版和轻量版三种。此处选择专业版。|
    |边缘版本|选择Link IoT Edge的[发布版本](../cn.zh-CN/产品简介/发布历史.md#)。|

3.  复制操作系统命令备用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103158/155505041544212_zh-CN.png)

4.  登录您的Ubuntu系统机器。
5.  任意目录下执行步骤3中已复制的命令。

    该命令实现一键下载、配置并启动Link IoT Edge。命令执行完成后，会在当前目录中下载link-iot-edge-standard.sh脚本。

    -   如果第一次启动Link IoT Edge，则需要完成如下交互式配置，您可以直接按**Enter**键使用默认配置。

        -   确认启动版本
        -   确认函数计算的runtime类型，默认为进程版
        -   确认是否启动流式计算，默认开启流式计算
        -   确认是否卸载之前已安装的版本，默认卸载
        拉取Docker镜像完成并启动可能需要等待5 ~ 10分钟，启动完成后通过docker ps命令查看相关Docker容器是否已启动，若系统显示如下图所示信息，表示启动成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103166/155505041537202_zh-CN.png)

    -   如果不是第一次安装启动Link IoT Edge，可使用已下载的link-iot-edge-standard.sh脚本，对Link IoT Edge进行重启、停止、获取状态、修改配置参数等操作，命令详情请见下图：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/155505041544210_zh-CN.png)

6.  在[物联网控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，查看网关状态。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103166/155505041537203_zh-CN.png)

7.  在实例详情页面中，查看CPU使用率、内存使用率、存储使用率以及实例进程需要授权访问阿里云云监控（CloudMonitor）服务。
    1.  请参考[云资源访问](../cn.zh-CN/用户指南/云资源访问.md#)内容，在[RAM控制台](https://ram.console.aliyun.com)，创建授信**IoT物联网**的服务角色，并为该角色添加名为**AliyunCloudMonitorFullAccess**的访问云监控服务的权限。
    2.  在**实例信息**页签下打开**云监控状态**，如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/155505041537199_zh-CN.png)

    3.  在实例进程后，单击**查看**，可查看实例各个进程的信息及CPU、内存使用率。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/155505041637200_zh-CN.png)

8.  您可以在**实例详情**页面，网关名称右侧的操作栏中单击**远程连接**或者**远程文件管理**，方便您远程控制网关设备或对网关设备上的文件进行管理。详细说明请参见[远程服务访问](../cn.zh-CN/用户指南/远程运维管理/远程服务访问.md#)。

## Link IoT Edge的其它操作 {#section_kpt_4wm_lgb .section}

-   重新配置 Link IoT Edge。

    如果您希望对当前已安装的 Link IoT Edge版本配置进行修改可以使用如下命令：

    ```
    ./link-iot-edge.sh --reconfig {Version}
    ```

    其中，\{Version\}替换为目标版本号，例如目标版本号为v1.8.2，则实际命令为`./link-iot-edge.sh --reconfig v1.8.2`。

-   停止Link IoT Edge。

    使用如下命令可以停止所有Link IoT Edge运行的容器，但是不会删除。

    ```
    ./link-iot-edge.sh --stop
    ```

-   重新启动Link IoT Edge。

    在容器已存在且没有运行的状态下，执行如下命令可重新启动Link IoT Edge。

    ```
    ./link-iot-edge.sh --restart {Version}
    ```

    其中，\{Version\}替换为目标版本号，例如目标版本号为v1.8.2，则实际命令为`./link-iot-edge.sh --restart v1.8.2`。

-   清理Link IoT Edge。

    执行如下命令可停止当前运行的Link IoT Edge相关容器 ，并会删除所有已安装的相关镜像，删除相关数据卷以及启动配置文件。

    ```
    ./link-iot-edge.sh --clean
    ```

-   提取Link IoT Edge的日志。

    执行如下命令可打包Link IoT Edge的所有日志，并拷贝到当前目录。

    ```
    ./link-iot-edge.sh --packagelog
    ```


## 下一步 {#section_g2c_bsp_fhb .section}

环境搭建完成后，您可以参考[设备接入](../cn.zh-CN/用户指南/设备接入/设备接入简介.md#)章节内容，把您的设备接入到物联网边缘计算。

