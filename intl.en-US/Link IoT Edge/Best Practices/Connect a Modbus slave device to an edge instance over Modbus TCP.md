---
keyword: [Modbus TCP, connect Modbus slave devices, Modbus]
---

# Connect a Modbus slave device to an edge instance over Modbus TCP

Modbus is a communication protocol based on the master/slave model. The master device requests data from slave devices. The Modbus driver of a gateway serves as the master device, and devices that connect to the gateway through the Modbus driver serve as slave devices. After the master device sends a query message to a slave device, the slave device sends a response message.

## Preparations

1.  A Ubuntu 16.04 x86\_64 system is prepared to run a gateway.

2.  A Windows host is prepared to run a Modbus slave simulator.

3.  Download a Modbus slave simulator from the URL of [Modbus tools](https://www.modbustools.com/download.html) and install the simulator on the Windows host.

4.  Check the firewall settings of the Windows host and make sure that access to the Modbus slave device is allows through port 502. If the access is denied, disable the firewall or change firewall settings to allow access to the port.

5.  Create an edge instance and enable a gateway. For more information, see [Build an environment](/intl.en-US/Link IoT Edge/User Guide/Set up environments/Link IoT Edge Pro Edition/Install Link IoT Edge on Ubuntu 16.04.md).


## Step 1: Assign a Modbus driver to the edge instance

1.  Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list).

2.  In the left-side navigation pane, click **Edge Instances**, and click **View** next to the required edge instance.

3.  Assign the required Modbus driver to the edge instance based on the CPU of the related gateway. For more information, see [Modbus drivers](/intl.en-US/Link IoT Edge/User Guide/Connect devices to Link IoT Edge/Official drivers/Modbus drivers.md).

    ![Select a driver](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p48381.png)

4.  On the Instance Details page of the edge instance, click the name of the assigned driver. Then, click **Driver Configurations** in the Devices section.

5.  In the Driver Configurations panel, click **Add Channel**. In the Add Channel panel, set the required parameters to add a channel to the Modbus driver.

    For more information about the parameters, see [Modbus driver configurations](/intl.en-US/Link IoT Edge/User Guide/Connect devices to Link IoT Edge/Official drivers/Modbus drivers.md).

    ![Add a channel](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p35187.png)


## Step 2: Assign a sub-device to the Modbus driver

1.  In the Devices section, click **Assign Sub-device**. In the Modbus driver settings, assign a device to the edge instance.

    You can select an existing Modbus device or create a new device. To create a device, follow these steps:

    **Note:** If you want to select an existing device, the device must be connected to a gateway by using the Modbus protocol. For more information, see [Create a product](/intl.en-US/Device Connection/Create a product.md).

2.  On the Assign Sub-device page that appears on the right side of the console, click **Add Sub-device**.

    ![Add Sub-device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p37903.png)

3.  In the Add Device dialog box, click **Create Product** to create a product to which the Modbus device belongs.

    ![Create a product (living room lamp)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p37904.png)

4.  In the Create Product dialog box, specify the required parameters, and click **OK**.

    ![Create a product](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p48524.png)

    |Parameter|Description|
    |---------|-----------|
    |Product Name|The name of the product. The product name must be unique for the current account. The product name must be 4 to 30 characters in length, and can contain letters, digits, underscores \(\_\), hyphens \(-\), at signs \(@\), and parentheses \(\).|
    |Gateway Connection Protocol|The communications protocol. You must set this parameter to Modbus.|
    |Authentication Mode|The authentication method. Select an authentication method that is suitable for your device. For more information, see [Overview](/intl.en-US/Device Connection/Authenticate devices /Overview.md).|
    |Product Description|The description of the product. This parameter is optional.|

5.  In the Add Device dialog box, the new product is automatically specified in the drop-down list of the Product section. Click Configure to add a custom feature to the product. For more information, see [Add a TSL feature](/intl.en-US/Device Management/TSL/Add a TSL feature.md).

    ![Add a custom feature to the Modbus product](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1711989851/p63920.png)

6.  In the Add Self-defined Feature dialog box, click Properties and set the required parameters. Then, click **Add Extended Information**.

    In the Add Extended Information dialog box, set the required parameters to specify the data points of the Modbus sub-device.

    ![Add extended information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2711989851/p35181.png)

    Set the Register Address parameter based on the data points of the simulated Modbus slave device, as shown in the following figure. In this example, three attributes named aaa, bbb, and ccc are created. These attributes correspond to the data points 0, 1, and 2 of the Modbus slave device.

    ![Data points of the simulated device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4919967161/p35182.png)

7.  Go to the **Add Device** dialog of the Instance Details page in the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). Then, add a Modbus device.

    ![Add a sub-device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2711989851/p70931.png)


## Step 3: Configure and deploy the edge instance

1.  Assign the new Modbus device to the edge instance.

2.  After the device is assigned to the edge instance, click **Device Configurations** in the Actions column of the device. Then, use a channel to associate the device with the Modbus driver.

    ![Configure a device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2711989851/p49270.png)

    |Parameter|Description|
    |---------|-----------|
    |Associated Channel|Select the channel that you have added in the [Step 1: Assign a Modbus driver to the edge instance](#section_3o0_ngn_roq) section.|
    |Device Station Number|To view the value, check the ID of the Modbus slave device in Step 6 of the [Step 2: Assign a sub-device to the Modbus driver](#section_vp0_c2k_2sy) section. In this example, the value of this parameter is 1.|

3.  On the Instance Details page, click **Deploy** in the upper-right corner of the page to deploy the edge instance.

4.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/). In the left-side navigation pane, choose **Devices** \> **Devices**. On the Devices page, click **View** next to the required Modbus product.

    On the Device Details page, choose **TSL Data** \> **Status**. On the Status tab, view the properties of the Modbus product.

    ![Status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3711989851/p35189.png)


