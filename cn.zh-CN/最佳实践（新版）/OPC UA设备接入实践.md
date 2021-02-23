OPC UA设备接入实践 
=================================

本文介绍基于OPC UA协议的终端设备（以下统称设备）接入边缘一体机，并与云端交互的方法。

前提条件 
-------------------------

* 已购买边缘一体机。

  

* 已激活您的边缘一体机。具体操作，请参见[边缘一体机安装与激活](/cn.zh-CN/安装激活/边缘一体机安装与激活.md)。

  




步骤一：搭建OPC UA Server 
----------------------------------------

OPC UA Server的环境依赖如下表格所示：


|  依赖组件  |   版本要求   |            安装命令             |
|--------|----------|-----------------------------|
| python | ≥ 3.5.2  | 无                           |
| pip    | ≥ 9.0.1  | 无                           |
| opcua  | ≥ 0.98.3 | `pip install opcua==0.98.3` |



本文以OPC UA Server模拟一个LED灯设备，该设备具有温度（temperature）属性，高温报警（high_temperature）事件。请根据以下步骤，完成OPC UA Server的搭建。

1. 下载OPC UA Server。

       wget http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/opcua_simulation_server.tar.gz

   

2. 启动OPC UA Server。

       tar -zxvf opcua_simulation_server.tar.gz
       cd opcua_simulation_server && ./opcua_simulation_server.sh

   




步骤二：安装OPC UA客户端 
------------------------------------

本文使用物联网边缘计算提供的官方OPC UA驱动接入OPC UA设备。在设备接入过程中的设备配置操作，需要借助OPC UA客户端作为辅助工具，获取OPC UA Server模拟设备信息，用于在控制台创建产品和配置驱动时使用。

本示例使用OPC UA客户端UaExpert工具。

1. 下载并安装OPC UA客户端UaExpert工具。具体操作，请参见[Unified Automation UaExpert工具文档](https://www.unified-automation.com/products/development-tools/uaexpert.html)。

   

2. 安装完成后打开UaExpert工具。

   ![UaExpert工具](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1312204061/p41036.png)
   

3. 在工具栏中单击![新版-opcua工具+图标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1312204061/p177821.png)图标，新增OPC UA Server。

   ![新增OPC UA Server](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1312204061/p41037.png)

4. 填写OPC UA Server的URL地址，建立与OPC UA Server的连接。URL为`OPC UA Server所在主机的IP地址:端口号`。

   **说明**

   OPC UA Server示例中默认监听端口为`4840`，因此OPC UA Server的URL地址格式示例如下： 

       opc.tcp://192.168.1.1:4840

   

   ![opcua server连接url ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1312204061/p41038.png)
   

5. 配置完成URL地址后单击 **OK** ，显示设备信息。

   ![opcua设备信息 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1312204061/p41040.png)

   设备信息包括以下内容：
   * 设备描述信息（图示中①）

     
   
   * 设备引用信息（图示中②）

     
   

   




步骤三：创建基于OPC UA协议的设备 
----------------------------------------

1. 登录[物联网平台控制台](http://iot.console.aliyun.com/)。

   

2. 创建 **节点类型** 为 **网关子设备** 、 **接入网关协议** 为 **OPC UA** 的产品。具体操作，请参见[创建产品](/cn.zh-CN/设备接入/创建产品.md)。

   ![创建opcua产品 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41049.png)

   其中，部分参数设置如下：
   

   |   参数   |                  描述                   |
   |--------|---------------------------------------|
   | 所属品类   | 选择 **标准品类** 下的 **边缘计算** \> **其他设备** 。 |
   | 节点类型   | 选择 **网关子设备** 。                        |
   | 接入网关协议 | 选择 **OPC UA** 。                       |

   

3. 创建产品完成后，在 **产品详情** 页为OPC UA产品添加如下自定义功能，然后发布上线自定义功能。具体操作，请参见[单个添加物模型](/cn.zh-CN/设备管理/物模型/单个添加物模型.md)。

   * 添加属性

     1. 根据下图所示，设置属性参数。

        ![添加属性-1 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41068.png)
        
     
     2. 设置参数完成后，单击 **新增扩展描述** ，配置节点名称。

        ![添加属性-2 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41069.png)

        **节点名称** ：设备在OPC UA Server中的变量节点 **DisplayName** 的值。

        ![设备的DisplayName ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p44726.png)
        
     

     
   
   * 添加服务

     1. 根据下图所示，设置服务参数。

        ![添加服务-1 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41070.png)
        
     
     2. 单击 **输入参数** 下的 **增加参数** ，为产品服务新增参数。

        ![添加服务-2 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41071.png)
        
     
     3. 设置参数完成后，单击 **新增扩展描述** ，配置节点名称。

        ![添加服务-3 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41072.png)

        **节点名称** ：设备method在OPC UA Server中的变量节点 **DisplayName** 的值。

        ![method的DisplayName ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p44729.png)
        
     

     
   
   * 添加事件

     1. 根据下图所示，设置事件参数。

        ![添加事件-1 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41073.png)
        
     
     2. 单击 **输出参数** 下的 **增加参数** ，为产品事件新增参数。

        ![添加事件-2 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41074.png)
        
     
     3. 设置参数完成后，单击 **新增扩展描述** ，配置节点名称。

        ![添加事件-3 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41075.png)

        **节点名称** ：设备事件在OPC UA Server中的变量节点 **DisplayName** 的值。

        ![high_temperature的DisplayName ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p44731.png)
        
     

     
   

   

4. 为OPC UA产品添加设备。具体操作，请参见[单个创建设备](/cn.zh-CN/设备接入/创建设备/单个创建设备.md)。

   ![添加设备 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312204061/p41076.png)
   




步骤四：配置终端设备 
-------------------------------

1. 登录[边缘计算控制台](https://iotedge.console.aliyun.com)。

   

2. 在左侧导航栏选择 **节点管理** \> **终端设备管理** 。

   

3. 在 **终端设备管理** 页面中，找到前提条件中激活的主机，选择 **通用设备** \> **+驱动** 。

   

4. 分配官方OPC UA驱动到主机中。

   ![opcua驱动](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7049250161/p213088.png)
   

5. 选择 **OPCUA** 驱动，单击 **设备列表** 区域框中的 **驱动配置** ，在弹出面板中单击 **添加通道** ，设置通道参数。

   ![新版-opcua驱动添加通道](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4112350161/p177861.png)

   部分参数说明如下所示。更多信息，请参见[添加OPC UA协议设备]()。
   

   |    参数    |               描述               |            配置举例            |
   |----------|--------------------------------|----------------------------|
   | 通道名称     | OPC UA通道名称。                    | opcua_server               |
   | 通道地址     | OPC UA Server的URL地址。           | opc.tcp://192.168.1.1:4840 |
   | 用户名      | OPC UA Server连接用户名。            | demo                       |
   | 密码       | OPC UA Server连接密码。             | abc123                     |
   | 方法调用超时时间 | 请求调用OPC UA Server的调用超时时间，单位为秒。 | 10                         |

   

6. 单击 **设备列表** 区域框中的 **添加设备** ，为OPC UA驱动关联已创建好的OPC UA产品和设备，然后单击 **确定** 。

   **说明**

   **设备名称** 下，需要您手动输入已创建的设备名称。

   ![新版-为opcua驱动关联终端设备](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4112350161/p177864.png)
   

7. 分配设备成功后，单击设备名称右侧的 **设备配置** 。

   根据参数说明配置参数后，单击 **确定** 。

   ![新版-opcua驱动设备配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4112350161/p177867.png)
   

   |  参数  |                                            描述                                             |
   |------|-------------------------------------------------------------------------------------------|
   | 关联通道 | 选择已添加的通道。                                                                                 |
   | 节点路径 | 设备在OPC UA Server中，从Objects开始到设备节点的绝对路径。例如demo_led设备在OPC UA Server中的路径为`Objects/demo_led`。 |

   

8. 在 **节点管理** 页面 **主机管理** 页签下，单击主机列表中操作栏中的 **主机** **部署** ，部署边缘一体机及其关联的所有资源。

   ![主机部署](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4112350161/p213090.png)
   

9. 在 **终端设备管理** 页签下，选择 **OPCUA** 驱动，查看设备状态显示为 **在线** ，表示已部署成功。

   




至此，您已完成OPC UA设备接入实践。
