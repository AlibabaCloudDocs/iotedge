# 基于Ubuntu 16.04搭建环境 {#task_1495784 .task}

本文介绍基于Ubuntu 16.04系统，如何快速将网关连接到物联网边缘计算控制台，并将网关数据上传至云端。

Link IoT Edge标准版软件包支持在Ubuntu 16.04 ~ Ubuntu 18.04系统上运行，并在下列平台上进行测试和验证：

|架构|操作系统|
|--|----|
|x86\_64|Ubuntu 16.04 ~ Ubuntu 18.04|
|ARMv7|Ubuntu 16.04 ~ Ubuntu 18.04|
|ARMv8（AArch64）|Ubuntu 16.04 ~ Ubuntu 18.04|

尽管Link IoT Edge可以在其它版本的Ubuntu操作系统上运行，但为了最佳的稳定性和安全性，建议您选择在官方支持的系统版本上运行。接下来，我们将基于x86\_64 Ubuntu 16.04的平台上为您介绍Link IoT Edge标准版安装部署的方法。Ubuntu16.04~18.04系统在其它架构上的标准版软件包您可以在[下载地址](../cn.zh-CN/产品简介/发布历史/下载地址.md#)中获取。

## 准备工作 {#section_g3g_eyn_n2l .section}

准备Ubuntu 16.04系统的PC或者虚拟机，并且该PC或者虚拟机能够正常连接网络。如果您不熟悉Ubuntu 16.04的安装，可参考[Ubuntu 16.04安装指南](https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop-1604#0)。

## 环境设置 {#section_etf_d9j_q8m .section}

在x86\_64 Ubuntu 16.04机器上需要设置Link IoT Edge运行所依赖的环境。

1.  在x86\_64 Ubuntu 16.04机器的本地终端窗口或者SSH终端窗口执行以下命令，下载环境检查工具并运行。 

    ``` {#codeblock_vr5_w7l_xmv}
    wget http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/testingTool/link-iot-edge_env-check.sh
    sudo chmod +x ./link-iot-edge_env-check.sh
    sudo ./link-iot-edge_env-check.sh
    ```

    **说明：** link-iot-edge\_env-check.sh脚本在Link IoT Edge支持的平台需要以root权限运行并需要以下Linux系统命令：printf、echo、cat、ls、expr、grep、test、uname、set、head、sort、cut、uniq、xargs、ifconfig。

2.  按照运行环境检查工具的提示在您的机器上安装所有必需的依赖项，当检查工具成功运行完成后，返回如下图信息，表示Link IoT Edge能够在您的机器上成功运行。 

    ![1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156826944338243_zh-CN.png)


## 创建边缘实例和网关 {#section_e7q_nbs_e0t .section}

1.  [物联网平台控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**。
2.  创建一个边缘实例。 
    1.  单击**新增实例**，在弹出窗口中设置**实例名称**。
    2.  在**网关产品**后单击**新建网关产品**，为实例创建网关。 物联网边缘计算中的网关，承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![创建网关产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156826944337158_zh-CN.png)

    3.  在新建产品页面中，设置网关产品参数，然后单击**完成**。 物联网边缘计算中的新建网关产品继承物联网平台 **设备管理** \> **产品**中的产品功能，已自动为您简化创建适合物联网边缘计算中使用的网关产品步骤。

        ![创建产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156826944337159_zh-CN.png)

        |参数|说明|
        |--|--|
        |产品名称|为网关产品设置名称，用于后续的查询及识别网关产品。支持中文、英文字母、数字和下划线，长度限制4~30，一个中文汉字算2位。|
        |所属分类|选择品类，为该产品定义[物模型](../cn.zh-CN/用户指南/产品与设备/物模型/什么是物模型.md#)。 可选择为：

         -   **自定义品类**：需根据实际需要，定义产品功能。
        -   任一既有功能模板。

选择任一物联网平台预定义的品类，快速完成产品的功能定义。选择产品模板后，您可以在该模板基础上，编辑、修改、新增功能。

 若您需要的网关没有特殊功能定义，建议您选择**自定义品类**。

 |
        |产品描述|可输入文字，用来描述产品信息。字数限制为100。可以为空。|

        产品创建成功后，页面自动跳转回新增实例页面，并且**网关产品**参数下自动分配了刚创建的网关产品。

    4.  在新增实例页面，单击**网关设备**后的**新建网关设备**为网关产品添加设备。 物联网边缘计算中的新建网关设备功能继承物联网平台 **设备管理** \> **设备**的功能。

        ![新建网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156826944337160_zh-CN.png)

    5.  根据界面提示设置参数后，单击**确认**。 

        |参数|描述|
        |--|--|
        |产品|系统已自动关联上一步创建的网关产品。|
        |设备名称|为该网关设备命名。设备名称需保持产品内唯一。如不填写，系统将自动生成。 **说明：** 设备名称支持大写字母\[A-Z\]、小写字母\[a-z\]、数字\[0-9\]和下划线（\_）。且不能以下划线开头或结尾。

 |

    6.  根据所搭建的环境，选择对应的Link IoT Edge产品规格，详细介绍请参见[产品规格](../cn.zh-CN/产品简介/产品规格.md#)。
    7.  （可选）在新增实例页面，单击**新增标签**，可以设置实例标签。通过标签您可以更加有效地归类及识别实例。您也可以不设置标签。
3.  实例参数设置完成后，单击**确定**，至此您已创建边缘实例和网关。

## 启动Link IoT Edge {#section_n2l_4ax_8u0 .section}

1.  在左侧导航栏中选择**边缘计算** \> **边缘实例**，单击实例名称右侧的**软件安装**。 

    ![下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156826944344201_zh-CN.png)

2.  根据环境设置下载参数，然后单击**生成安装命令**。 

    ![生成下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156826944351766_zh-CN.png)

    |参数|描述|
    |--|--|
    |CPU架构|您的设备系统对应的CPU架构。此处选择x86-64。|
    |产品规格|在创建边缘实例时，已选择实例中使用的Link IoT Edge版本。此处不可操作。|
    |边缘版本|选择Link IoT Edge的[发布版本](../cn.zh-CN/产品简介/发布历史/专业版.md#)。|
    |操作系统|选择您的设备对应的操作系统。此处选择Linux。|

    如果您暂时没有合适的硬件载体来运行Link IoT Edge，您可以单击对话框上方的**立即体验**，使用Cloud Shell虚拟机快速体验标准版Link IoT Edge的产品功能。使用**立即体验**功能有诸多注意事项，详情请参见[基于阿里云Cloud Shell快速体验Link IoT Edge](cn.zh-CN/用户指南/环境搭建/标准版环境搭建/基于阿里云Cloud Shell搭建环境.md#)。

    **说明：** 同一个边缘实例只能启动一个Link IoT Edge，若在已经商用的边缘实例（即边缘实例已在硬件网关上启动了Link IoT Edge）使用**立即体验**功能时，会导致硬件网关上启动的Link IoT Edge和虚拟机上启动的Link IoT Edge不断互踢，影响您的正常业务。强烈建议您不要在已启动Link IoT Edge的边缘实例上使用**立即体验**功能。

3.  复制操作系统命令备用。 

    ![标准版linux复制命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156826944451767_zh-CN.png)

4.  登录您的x86\_64 Ubuntu 16.04机器。
5.  任意目录下执行步骤3中已复制的命令。 该命令实现一键下载、配置并启动Link IoT Edge。命令执行完成后，会在当前目录中下载link-iot-edge-standard.sh脚本。

    **说明：** 如果不是第一次安装启动Link IoT Edge，可使用已下载的link-iot-edge-standard.sh脚本，对Link IoT Edge进行重启、停止、获取状态、修改配置参数等操作，命令详情请见下图：

    ![其他操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156826944444213_zh-CN.png)

6.  执行如下命令查看Link IoT Edge核心服务的运行状态。 

    ``` {#codeblock_xs7_rcg_ie3}
    sudo ./link-iot-edge-standard.sh --status
    ```

    若系统显示如下信息，表示Link IoT Edge核心服务启动成功。

    ![网关启动成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156826944444214_zh-CN.png)

    您也可以在[物联网控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例** ，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，选择**网关**，查看网关状态。

    ![网关在线](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156826944448660_zh-CN.png)

7.  （可选）在实例详情页面，查看CPU使用率、内存使用率、存储使用率以及实例进程需要授权访问阿里云云监控（CloudMonitor）服务。 
    1.  请根据[云资源访问](../cn.zh-CN/用户指南/云资源访问.md#)内容，添加角色或分配已有的角色，并为该角色添加**管理云监控（CloudMonitor）的权限**。
    2.  选择**设置**页签，在实例信息中打开**云监控状态**按钮，如下图所示。 

        ![打开云监控](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/301656/156826944448668_zh-CN.png)

        云监控状态打开后，可在实例详情页面选择**监控信息**，查看网关的各类监控信息。

8.  （可选）在实例详情页面选择**设置**，打开**远程访问**按钮后，可对网关进行远程管理，详细操作步骤请参见[远程服务访问](../cn.zh-CN/用户指南/远程运维管理/远程服务访问.md#)。

## 使用systemd管理Link IoT Edge {#section_5h8_i4m_1lx .section}

您可以使用systemd来管理Link IoT Edge服务的启动（start）、停止（stop）和查看状态（status）。

Link IoT Edge的systemd service如下所示：

```
[Unit]
Description=Link IoT Edge

[Service]
Type=forking
Restart=on-failure
ExecStart=/linkedge/gateway/build/script/iot_gateway_start.sh
ExecReload=/linkedge/gateway/build/script/iot_gateway_start.sh
ExecStop=/linkedge/gateway/build/script/iot_gateway_stop.sh

[Install]
WantedBy=multi-user.target
```

您可运行如下命令配置开机自启动功能。

```
wget http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/testingTool/LinkIoTEdge.service
sudo cp LinkIoTEdge.service /etc/systemd/system/LinkIoTEdge.service
sudo systemctl enable LinkIoTEdge.service
```

其他常用命令。

-   启动命令：`sudo systemctl start LinkIoTEdge.service`
-   重启命令：`sudo systemctl restart LinkIoTEdge.service`
-   停止命令：`sudo systemctl stop LinkIoTEdge.service`
-   禁用开机自启动：`sudo systemctl disable LinkIoTEdge.service`

## 下一步 {#section_ufa_drh_uyh .section}

环境搭建完成后，您可以根据[设备接入](../cn.zh-CN/用户指南/设备接入/设备接入简介.md#)章节内容，把您的设备接入到物联网边缘计算。同时也可以为边缘实例分配其他资源（如函数计算、消息路由等）管理您的设备。

接入设备或分配其他资源到边缘实例后，需要根据如下步骤部署边缘实例。

1.  在实例详情页面，单击右上角**部署**后在弹出框中单击**确定**，部署边缘实例。
2.  当部署状态显示为**部署成功**，表示部署实例完成。您可以单击**查看日志**，查看部署详情。 

    ![查看部署日志](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/301656/156826944448671_zh-CN.png)


