---
keyword: [Sample drivers, LightSensor driver, Light driver]
---

# Sample drivers

This topic describes two sample drivers provided by Link IoT Edge: Light and LightSensor. It also provides details about how to use these drivers.

The Light driver is a driver that is designed for smart lamps. You can use the Light driver to simulate and control smart lamps.

The LightSensor driver is a driver that is designed for light sensors. You can use this driver to simulate light sensors. This driver allows the simulated light sensors to repeat light intensity data based on a specified cycle.

## Method of using sample drivers

1.  Assign the Light driver and a sub-device to an edge instance.

    1.  On the **Instance Details** page, click the Devices & Drivers tab, and click the `+` icon on the right side of **All Drivers**. Then, select **Official Drivers** from the drop-down list, and assign the Light driver to the edge instance.

        ![Assign the Light driver to an edge instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6922378851/p37907.png)

    2.  Optional. Configure the driver. To do this, click the Light driver, and click **Driver Configurations** next to **Devices**. After you complete the configuration, click **OK**.

        In this example, you do not need to configure the driver.

        ![Configure the sample driver](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6922378851/p48030.png)

        |Parameter|Description|
        |---------|-----------|
        |Configuration Format|The configuration method. Valid values:         -   Key-value Configuration
        -   JSON Format
        -   Configuration File |
        |Configuration Format \(Key-value Configuration\)|If you select **Key-value Configuration**, click **Add Configuration** on the Driver Configurations page. Then, specify the Configuration Name, Value, and Description parameters. You can add a maximum of 100 key-value pairs. |
        |Configuration Format \(JSON Format\)|If you select **JSON Format**, enter the JSON-formatted data to configure the driver. The data size cannot exceed 1 KB. Link IoT Edge automatically verifies the format. If the format is invalid, modify the data as prompted.|
        |Configuration Format \(Configuration File\)|If you select **Configuration File**, edit a local configuration file and upload it to the console.|

    3.  Optional. On the right side of Devices, click **Container Configurations**. On the page that appears, configure the container for the driver. After you complete the configuration, click **Save**.

        **Note:** You can specify Container Configurations only when the **Instance Type** parameter is set to Pro Edition.

        |Parameter|Description|
        |---------|-----------|
        |Host Mode|Specifies whether to isolate the container network from the host network. The valid values are described as follows:         -   Yes: This value indicates that the container network is the same as the host network.
        -   No: This value indicates that the container network is isolated from the host network. If you select this option, you must configure the Network Port Mapping settings. |
        |Network Port Mapping|The mappings between host network ports and container network ports. This parameter is available only whenHost Mode is set to No. The network where the function runs is isolated from the host network. You can map the listening port of the function in the container to a host network port. This allows client programs on various hosts to access the services that are provided by the function. You can specify a maximum of 10 entries. For example, the `fc-http-server` function runs in a host container, and provides services by using socket port 80. The client programs on other hosts cannot access the `fc-http-server` function by accessing port 80 on the current host. To enable the client programs on other hosts to access the `fc-http-server` function, you must map the network port \(port 80\) in the container where the function runs to a host network port, such as port 8080. Then, the client programs on other hosts can access the `IP address:port 8080` in the host network, and use the services provided by the `fc-http-server` function. |
        |Privilege Mode|Specifies whether to enable the privilege mode. Root users of containers can access host services only as general users. If you want to change the system time or run the mount command in containers, you must be granted the required root permissions. In this scenario, you must enable the privilege mode for the containers.

 **Note:** If you enable the privilege mode, applications and programs in the containers are granted the host root permissions, and all the host devices are mapped to the containers. Therefore, you do not need to configure the Device Mapping settings. |
        |Device Mapping|The device mappings. This parameter is available only when you select No for Privilege Mode. The network where the device management system resides is isolated from the host network. To enable a function to access a host device such as a serial interface, you must map the device to the container where the function runs. You can specify a maximum of 10 entries.|
        |Volume Mapping|The volume mappings. The network where the file system resides is isolated from the host network. To enable a function to access a host file, you must map the file to the container where the function runs. You can specify a maximum of 10 entries.|

    4.  In the Devices section, click **Assign Sub-device**. In the Light driver settings, assign a device to the edge instance.

        ![Assign a sub-device to the sample driver](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6922378851/p48037.png)

        On the Assign Sub-device page that appears on the right side of the console, click **Add Sub-device**.

        ![Add Sub-device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p37903.png)

    5.  In the Add Device dialog box, click **Create Product** to create a product named Living\_Room\_Lamp.

        ![Create a product (living room lamp)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p37904.png)

        In the Create Product dialog box, specify the required parameters, and click **OK**.

        ![Configure parameters for the living room lamp](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7922378851/p37905.png)

        |Parameter|Description|
        |---------|-----------|
        |Product Name|The name of the product. In this example, this parameter is set to Living\_Room\_Lamp.|
        |Gateway Connection Protocol|The communications protocol that is used by the gateway. In this example, select Custom.|
        |Authentication Mode|The authentication method. Select an authentication method that is suitable for your device. For more information, see [Overview](/intl.en-US/Device Access/Authenticate devices /Overview.md).|

    6.  In the Add Device dialog box, set the DeviceName parameter to **Light** and click **OK**. The Living\_Room\_Lamp value is automatically filled in the Product parameter.

        ![Add the living room lamp](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7922378851/p38329.png)

    7.  In the Assign Sub-device dialog box, assign the Light device of the Living\_Room\_Lamp product to the edge instance.

        ![Assign the living room lamp to the edge instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7922378851/p37906.png)

    8.  Assign the LightSensor driver to the edge instance. In the LightSensor settings, create and assign a product named Light\_Sensor and a device named LightSensor to the edge instance. The procedures are similar to those for assigning the Light driver and the device of the Living\_Room\_Lamp product to the edge instance.

        When you create the light sensor product, specify the required parameters as follows.

        |Parameter|Description|
        |---------|-----------|
        |Product Name|The name of the product. In this example, this parameter is set to Light\_Sensor.|

        Now you have assigned the LightSensor and Light devices to the edge instance.

    9.  Optional. Click **Device Configurations** in the Actions column for the assigned device. In the dialog box that appears, you can configure the device settings. For example, you can configure the device serial number, and the driver can then process the information from the specified device.

        In this example, you do not need to specify the device configurations.

        ![Device configurations](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7922378851/p48268.png)

        The size of the specified JSON-formatted data cannot exceed 1 KB. After the specified data passes the **format check**, click **OK**.

2.  Deploy the edge instance.

    In the upper-right corner of the Instance Details page, click **Deploy**. In the dialog box that appears, click **OK** to deploy the edge instance.

    You can check the deployment process and result by viewing **Deployment Process**.

3.  Check whether the device is in the **Online** state.

    To do this, click the **Devices & Drivers** tab on the **Instance Details** page. In the **All Drivers** section, find the status of the Light and LightSensor devices. The result shows that the two devices are in the Online state.

    ![Online devices](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7922378851/p37935.png)

4.  View the device running status.

    To do this, click **View** in the Actions column for the LightSensor or Light device. You are then directed to the Device Details page. To view the device details, you can also choose **Devices** \> **Devices**, and click the target device name. Then, click the **Thing Model Data** \> **Status** tab on the **Device Details** page. On this tab, you can find that the device data is sent to the cloud as expected.

    The following figure shows the LightSensor device status.

    ![LightSensor device status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7922378851/p37937.png)

    The following figure shows the Light device status.

    ![Light device status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8922378851/p37938.png)


Now you have connected the devices to the sample drivers. For more information about official drivers and driver development, see [Official drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Official drivers/Modbus drivers.md) and [Develop drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Develop drivers/Overview.md). For more information about business logic and frameworks, see [Edge applications](/intl.en-US/User Guide/Edge applications/What are edge applications?.md) and [Scene orchestration](/intl.en-US/User Guide/Scene orchestration/What is scene orchestration?.md).

