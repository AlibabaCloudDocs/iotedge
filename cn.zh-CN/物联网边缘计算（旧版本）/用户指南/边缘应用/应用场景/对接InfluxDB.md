# 对接InfluxDB

本文以一个典型的开源时序型数据库（InfluxDB）为例，描述如何使用边缘函数计算应用，实现时序存储设备数据。

-   请您确保已完成边缘实例的创建，具体操作，请参见[专业版环境搭建](/cn.zh-CN/物联网边缘计算（旧版本）/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md)。
-   您已创建光照度传感器产品以及该产品下的LightSensor设备，并将设备分配至边缘实例，具体操作，请参见[示例驱动](/cn.zh-CN/物联网边缘计算（旧版本）/用户指南/设备接入/示例驱动.md)。
-   您已创建容器镜像类型的边缘应用，具体操作，请参见[容器镜像应用](/cn.zh-CN/物联网边缘计算（旧版本）/用户指南/边缘应用/新增自研应用/容器镜像应用.md)。

    其中，部分参数设置按如下要求配置。

    |参数|说明|
    |--|--|
    |应用类型|此处选择容器镜像。|
    |仓库类型|此处选择公共仓库 。|
    |镜像地址|设置为`influxdb:latest`。|
    |应用版本|设置为当前使用的数据库版本号，例如1.7.9版本。|

    |参数|描述|
    |--|--|
    |是否使用宿主机host模式|此处选择否。|
    |网络端口映射|此处按如下说明，设置两条网络端口映射：     -   第一条网络端口映射：
        -   宿主机端口：8083
        -   容器内端口：8083
        -   类型：TCP
    -   第二条网络端口映射：
        -   宿主机端口：8086
        -   容器内端口：8086
        -   类型：TCP |
    |是否启动特权模式|此处选择是。|
    |卷映射|此处按如下说明，设置卷映射：     -   源路径：/tmp/influxdb
    -   目的路径：/var/lib/influxdb
    -   读写权限：读写 |


在楼宇、工业、农业等物联网场景中，现场的各类传感器负责实时采集数据（如温、湿度、空气质量等数据）。这些数据会随着时间的变化不断更新，因此也称之为时序数据。若需要对此类数据进行大数据分析和看板展示数据等操作，您首先需要将其存储到时序数据库中。

物联网边缘计算提供的函数计算应用能力，可帮助您快速地将模型化的设备数据存储到时序数据库中。在此过程中，只需配置该函数计算应用的消息路由并部署应用，无需二次开发。

本文中以LightSensor传感器为例，将获取到的LightSensor传感器数据，按照时间顺序存储到InfluxDB中。

## 步骤一：创建应用函数

1.  下载应用函数代码包[fcApp\_influxdb\_v1.0.zip](http://link-iot-edge-packet.oss-cn-shanghai.aliyuncs.com/fc-demo/fcApp_influxdb_v1.0.zip)。

2.  登录[函数计算控制台](https://fc.console.aliyun.com/)。

    如尚未开通该服务，请阅读并选中**我已阅读并同意**，单击**立即开通**，开通服务。

3.  （可选）在左侧导航栏单击**服务及函数**，在**服务及函数**页面**服务列表**区域，单击**新增服务**，创建一个服务。

    其中，**服务名称**必须填写，此处设置为EdgeFC，其余参数可根据您的需求设置，也可以不设置。

    **说明：**

    -   若您首次在函数计算中创建服务，请根据配置向导配置参数。
    -   若已操作过其他应用场景示例或小程序示例，即已创建EdgeFC服务，则无需重复创建。
4.  创建服务成功后，在服务与函数页面的EdgeFC区域，单击**新增函数**。

5.  在**新建函数**页面，单击**事件函数**区域中的**配置部署**。

6.  设置应用函数的基础管理配置参数。

    |参数|描述|
    |--|--|
    |函数类型|保持默认选项。|
    |所在服务|选择已创建的EdgeFC服务。|
    |函数名称|设置为influxdbStore。|
    |运行环境|设置函数的运行环境并选择上传代码的方式。此示例中选择Python 3。在**上传代码**右侧选择**上传代码包**，单击**上传代码**，上传步骤1中下载的[fcApp\_influxdb\_v1.0.zip](http://link-iot-edge-packet.oss-cn-shanghai.aliyuncs.com/fc-demo/fcApp_influxdb_v1.0.zip)代码包。 |
    |函数入口|使用默认值index.handler。|

    其余参数的值请根据您的实际需求设置，也可以不设置。更多信息，请参见[函数计算]()。

    确认函数信息后，单击**新建**完成操作。

7.  创建函数完成后，系统自动跳转到函数详情页面。您可在**代码执行**页签的**代码执行管理**区域下，选中**在线编辑**单选框，查看源码。

    ![在线编辑](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9499879851/p66268.png)

    **说明：** influxdbStore样例代码逻辑分为三步。

    1.  从收到的设备上报数据（event参数）中解析出productKey、deviceName和attribute。

        ```
        event_json = json.loads(event)
        if(event_json["topic"].startswith('/sys'))
          pk, dn, attribute = parseTopic(event_json['topic'])
        ```

    2.  解析payload（设备的属性或者事件）。

        ```
        
        payload_json = json.loads(event_json["payload"])
        ```

    3.  将属性或者事件数据封装成InfluxDB存储的格式，数据格式定义请参见本文下方[附录：数据格式定义](#section_5ct_vrz_mj1)。此处依赖了Python封装的InfluxDB客户端接口。

## 步骤二：分配函数到边缘实例

1.  登录[边缘计算控制台](https://iot.console.aliyun.com/le/instance/list)。

2.  在左侧导航栏单击**应用管理**。

3.  使用本文上方[步骤一](#section_urh_c0v_qdv)中已创建的函数，创建函数计算类型的边缘应用。具体操作，请参见[函数计算应用](/cn.zh-CN/物联网边缘计算（旧版本）/用户指南/边缘应用/新增自研应用/函数计算应用.md)。

    应用信息参数说明如下：

    |参数|描述|
    |--|--|
    |应用名称|设置您应用的名称，例如influxdbStore。|
    |应用类型|选择函数计算。|
    |地域|选择您创建的服务所在的地域。|
    |服务|选择EdgeFC服务。|
    |函数|选择influxdbStore函数。|
    |授权|选择AliyunIOTAccessingFCRole。|
    |应用版本|设置应用的版本，必须是该应用唯一的版本号，即一个应用不可以设置两个相同的版本号。|

    函数配置说明如下：

    |参数|描述|
    |--|--|
    |启用默认配置|选择否。|
    |运行模式|运行模式有两种。此处选择**持续运行**模式。程序部署后会立即执行。|
    |超时限制（秒）|函数收到事件后的最长处理时间，此处使用默认值5秒。如超过该时间函数仍未返回结果，该函数计算程序将会被强制重启。|
    |定时运行|使用默认配置：关闭。|
    |环境变量|单击**新增环境变量**，添加如下方“环境变量配置”表格所示的环境变量。|

    |名称|值|
    |--|--|
    |host|InfluxDB的访问地址。|
    |port|InfluxDB的访问端口，默认值为8086。|
    |username|InfluxDB的用户名，默认值为root。|
    |password|InfluxDB的密码，默认值为root。|
    |database|InfluxDB的数据库名称，默认值为example。|

    其余参数无需配置。

4.  在左侧导航栏单击**边缘实例**。

5.  在本文“前提条件”中创建的边缘实例右侧，单击**查看**。

6.  在**实例详情**页面的**边缘应用**页签，单击**分配应用**。

7.  在**分配应用**面板，找到已创建的应用函数influxdbStore，单击对应操作栏中的**分配**，然后单击**关闭**。


## 步骤三：配置消息路由

添加消息的详细步骤及各个参数的解释。详细信息，请参见[设置消息路由](/cn.zh-CN/物联网边缘计算（旧版本）/用户指南/消息路由/设置消息路由.md)。

1.  在实例详情页面，选择**消息路由**，单击**添加路由**，添加LightSensor设备到函数计算的消息路由。

2.  按照界面提示，设置如下参数，参数设置完成后，单击**确认**。

    |参数|描述|
    |--|--|
    |路由名称|设置一个消息路由名称。|
    |消息来源|此处选择**设备**，选择**光照度传感器** \> **LightSensor**。|
    |消息主题过滤|此处选择**全部**。|
    |消息目标|此处选择**边缘应用**和**EdgeFC/influxdbStore**函数。|


## 步骤四：部署边缘实例

1.  在实例详情页面，单击右上角**部署**后，在弹出对话框中单击**确定**，将子设备、函数计算等资源下发到边缘端。

2.  通过SSH登录您的网关，执行tail -f /linkedge/run/logger/fc-base/influxdbStore/log.INFO命令，可以查看该函数的日志，来观察其实际运行情况。

    ![代码片段](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9499879851/p66276.png)


## 附录：数据查询

当数据存储到InfluxDB后，可通过InfluxDB API查询已存储的数据。部分数据查询示例如下所示，更多详情，请参见[InfluxDB API文档](https://docs.influxdata.com/influxdb/v1.7/tools/api)。

-   以产品为维度，查询某个属性所有时间点的值，返回结果会以时间顺序列出所有已存储的属性值。

    ```
    curl -G 'http://localhost:8086/query?db=example&u=root&p=root' --data-urlencode "epoch=ms" --data-urlencode 'q=SELECT * FROM "属性唯一标识符（产品下唯一）" WHERE "_productKey" = $pk and "_dataType" = $type' --data-urlencode 'params={"pk":"产品ProductKey", "type": "property"}'
    
    //响应结果
    {
        "results": [{
            "statement_id": 0,
            "series": [{
                "name": "temp",
                "columns": ["time", "_dataType", "_deviceName", "_productKey", "value"],
                "values": [
                    [1570782663561, "property", "0987654321", "产品ProductKey", 100.1],
                    [1570782688527, "property", "0987654321", "产品ProductKey", 100.2],
                    [1570782851708, "property", "0987654321", "产品ProductKey", 104.4]
                ]
            }]
        }]
    }
    ```

-   以设备为维度，查询某个属性所有时间点的值，返回结果会以时间顺序列出所有已存储的属性值。

    ```
    curl -G 'http://localhost:8086/query?db=example&u=root&p=root' --data-urlencode "epoch=ms" --data-urlencode 'q=SELECT * FROM "属性唯一标识符（产品下唯一）" WHERE "_deviceName" = $dn and "_dataType" = $type' --data-urlencode 'params={"dn":"设备名称", "type": "property"}'
    ```

-   以设备为维度，查询某个属性在一定时间范围内的值，返回结果会以时间顺序列出该时间范围内所有已存储的属性值。

    ```
    curl -G 'http://localhost:8086/query?db=example&u=root&p=root' --data-urlencode "epoch=ms" --data-urlencode 'q=SELECT * FROM "属性唯一标识符（产品下唯一）" WHERE "_productKey" = $pk and "_dataType" = $type and "time" > $timestamp' --data-urlencode 'params={"pk":"产品ProductKey", "type": "property", "timestamp": "2019-10-11T09:03:15.611Z"}'
    ```


## 附录：数据格式定义

设备的属性或事件类型数据在InfluxDB的存储格式如下所示。

-   单值式属性

    ```
    [
        {
          "measurement": "temp",            // 属性名
          "tags": {                         // 属性的标签
            "_productKey": "1234567890",    // 设备证书信息productKey
            "_deviceName": "0987654321",    // 设备证书信息deviceName
            "_dataType"  : "property"       // 类型：property表示属性，event表示事件
          },
          "time": 1346846400000,            // 时间戳，单位：ms
          "fields": {
            "value": 123                    // 属性的值
          }
        }
        ...
    ]
    ```

-   结构体式属性

    ```
    [
        {
          "measurement": "temp",            // 属性名
          "tags": {                         // 属性的标签
            "_productKey": "1234567890",    // 设备证书信息productKey
            "_deviceName": "0987654321",    // 设备证书信息deviceName
            "_dataType"  : "property"       // 类型：property表示属性，event表示事件
          },
          "time": 1346846400000,            // 时间戳，单位：ms
          "fields": {
            "aa": 12,                       // 属性的值
            "bb": 12,                       // 属性的值
            "cc": 12,                       // 属性的值
            "dd": 12,                       // 属性的值
          }
        }
        ...
    ]
    ```

-   事件

    ```
    [
        {
          "measurement": "event123",        // 事件名
          "tags": {                         // 事件的标签
            "_productKey": "1234567890",    // 设备证书信息productKey
            "_deviceName": "0987654321",    // 设备证书信息deviceName
            "_dataType"  : "event"          // 类型：property表示属性，event表示事件
          },
          "time": 1346846400000,            // 时间戳，单位：ms
          "fields": {
            "speed" : 20.8,
            "level" : 4,
            "direction" : "East",
          }
        }
        ...
    ]
    ```


