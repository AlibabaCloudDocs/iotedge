---
keyword: [device simulator, simulator, DeviceSimulator]
---

# Device simulator

Link IoT Edge provides various features such as scene orchestration, function compute, and streaming data analysis to help you create IoT applications. Link IoT Edge also provides device simulators. It allows you to test applications without using physical devices that may not be available.

A device simulator consists of the following two components:

-   Driver: simulates all types of devices at the edge. The properties, events, services of devices are defined by [TSL](/intl.en-US/Device Management/TSL/What is a TSL model?.md).
-   Control tool: changes the property values of the device simulator and triggers the device simulator to submit events.

By performing the following operations, you can test applications without using physical devices: 1. Bind devices with device simulator drivers. 2. Assign the devices to the edge instance. 3. Use control tools to control the devices. The following sections describe how to use device simulators.

## Prerequisites

-   A device simulator driver is downloaded.

    |Link IoT Edge edition|Link IoT Edge version|Driver download URL|
    |---------------------|---------------------|-------------------|
    |Pro and Standard Edition|1.8.2 and later versions|[DeviceSimulator\_v0.2](http://link-iot-edge-packet.oss-cn-shanghai.aliyuncs.com/driver/DeviceSimulator_v0.2.zip)|

-   An edge instance is created. Device simulators are only applicable to Link IoT Edge Standard Edition and Link IoT Edge Pro Edition. For more information about how to create an edge instance, see [Build environments for Link IoT Edge Pro Edition](/intl.en-US/User Guide/Set up environments/Link IoT Edge Pro Edition/Install Link IoT Edge on Ubuntu 16.04.md) or [Build environments for Link IoT Edge Standard Edition](/intl.en-US/User Guide/Set up environments/Link IoT Edge Standard Edition/Install Link IoT Edge on Ubuntu 16.04.md).

## Use a device simulator driver

1.  Upload the driver.

    1.  In the left-side navigation pane of the [IoT Platform console](https://iot.console.aliyun.com/), choose **Link IoT Edge** \> **Drivers**.

    2.  On the Drivers page, click the Custom Drivers tab. Click **Create Driver**.

    3.  On the **Create Driver** page, configure the driver parameters and upload the driver file that you downloaded in [Prerequisites](#section_ntw_51v_tgb). For more information about how to create a driver, see [Publish cloud-hosted drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Publish drivers/Publish cloud-hosted drivers.md).

        The following figure shows the parameters to be configured in this example. You can specify values for other parameters based on your needs or leave parameters empty. For more information about how to specify parameters, see [Publish cloud-hosted drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Publish drivers/Publish cloud-hosted drivers.md).

        ![Create a driver](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3596789851/p38787.png)

    4.  Configure the parameters, upload the driver file, and click **OK**. You can view the new driver in the driver list.

2.  Assign the driver to the edge instance.

    1.  In the left-side navigation pane, choose **Link IoT Edge** \> **Edge Instances**. Find the edge instance that is created in [Prerequisites](#section_ntw_51v_tgb) and click **View** in the Actions column.

    2.  On the **Instance Details** page, click the Devices & Drivers tab. In the **All Drivers** section, click the `+` icon. In the dialog box that appears, select **Custom Drivers**. Find the DeviceSimulator driver that is created in the previous step and click **Assign**.

        ![Assign the driver to the edge instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3596789851/p38796.png)

    3.  Optional. If you have created a Link IoT Edge Pro Edition edge instance, you must configure container parameters.

        Select the DeviceSimulator driver. Click **Container Configurations** next to **Device List**. Configure the parameters and click **Save**.

        ![Configure container parameters](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3596789851/p75051.png)

        The following table describes the parameters of a port mapping. For more information about parameters, see [Sample drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Sample drivers.md).

        |Parameter|Description|
        |---------|-----------|
        |Host Port|Specifies a host port to which a container port is mapped. You must specify a host port that is not being used. Example: 8999.|
        |Container Port|You can only specify 9000 for this parameter.|
        |Type|Select TCP.|

3.  Add a sub-device to the edge instance.

    1.  In the **All Drivers** section, select DeviceSimulator. Click **Assign Sub-device**.

    2.  In the Assign Sub-device dialog box that appears, click **Add Sub-device**.

        ![Create a sub-device ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3596789851/p21102.png)

    3.  In the Add Device dialog box that appears, click **Create Product**.

        ![Create a product](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p38858.png)

    4.  In the Create Product dialog box, click **Complete**.

        ![Create a product](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p38771.png)

    5.  In the Add Device dialog box, click **Configure** to add TSL definitions.

        ![Add TSL definitions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p49011.png)

        -   Add a temperature property for the product. For more information about how to define a property, see [Add self-defined features](/intl.en-US/Device Management/TSL/Add a TSL feature.md).

            ![Define a property](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p38772.png)

        -   Add a high\_temperature event for the product. For more information about how to define an event, see [Add self-defined features](/intl.en-US/Device Management/TSL/Add a TSL feature.md).

            ![Define an event](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p38773.png)

            Add parameters for the event.

            ![Event parameters](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p38774.png)

    6.  Go to the Add Device dialog box, specify the **DeviceName** parameter, and click **OK**.

        ![Add a device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4596789851/p38776.png)

    7.  In the Assign Sub-device dialog box, select the **temperatureSensor** product. Find temperatureSensor01 and click **Assign**.

4.  Deploy the edge instance.

    On the Instance Details page, click **Deploy** in the upper-right corner. In the Deployment Process dialog box that appears, you can click **View Logs** to view deployment details. If the edge instance is deployed, the following state is displayed next to the instance name: **Deployed**.


## Use the control tool of the device simulator

The control tool of the device simulator is similar to buttons of a physical device. After performing the preceding steps in the [Use a device simulator driver](#section_ehh_2bv_tgb) topic, you can use the control tool.

1.  Log on to your remote terminal. For more information about how to log on to a remote terminal, see [Remote service access](/intl.en-US/User Guide/Remote OAM/Remote service access.md).

2.  Optional. If you are using Link IoT Edge Pro Edition, you must run the following command on the remote terminal to modify the configurations of the control tool.

    ```
    echo Host\_IP\_Address:Host\_Port > /linkedge/run/ds_ctrl.conf
    ```

    **Note:** Host IP Address specifies the host IP address of your edge gateway. Host Port specifies the host port that is specified in [step 2](#step_n3s_yoi_mf2) of the [Use a device simulator driver](#section_ehh_2bv_tgb) topic. In this example, port 8999 is specified.

3.  Use the control tool to control device behaviors.

    Go to the /linkedge/gateway/build/bin directory, and run the `./ds_ctrl` command to view the syntax.

    ```
    Usage: ds_ctrl <command>
    
    where <command> is one of:
        property, event
    
    ds_ctrl property productKey deviceName params            Change property
    ds_ctrl event productKey deviceName eventCode params     Trigger event
    
    
    For example(productKey = xxx, deviceName = yyy):
        ds_ctrl property xxx yyy '{"temperature":30}'
        ds_ctrl event xxx yyy alarm '{"temperature":90}'
    ```

    -   Change a device property
        1.  Change the temperature.

            Use the tool to change the sensor temperature to 30.

            ```
            ./ds_ctrl property a1WuxHr**** temperatureSensor01 '{"temperature":30}'
            ```

            The system returns the following message, indicating that the temperature is changed.

            ```
            Send property success!
            ```

        2.  In the left-side navigation pane of the [IoT Platform console](http://iot.console.aliyun.com/), choose **Devices** \> **Devices**. Find the required device and click **View** in the Actions column.

            On the Device Details page, click the **Thing Model Data** \> **Status** tab to view the running status of the device.

            ![Status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5596789851/p38799.png)

        3.  Optional. Simulate multiple temperature changes.

            Run the following command five times, and add the value by 1 each time.

            ```
            ./ds_ctrl property a1WuxHr**** temperatureSensor01 '{"temperature":31}'
            ```

            You can go to the **Thing Model Data** \> **Status** tab to view data changes.

            ![Status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5596789851/p38800.png)

    -   Trigger a device event
        1.  Submit an event if the temperature reaches a specified value.

            ```
            ./ds_ctrl event a1WuxHr**** temperatureSensor01 high_temperature '{"temperature":90}'
            ```

        2.  In the left-side navigation pane of the [IoT Platform console](http://iot.console.aliyun.com/), choose **Devices** \> **Devices**. Find the required device and click **View** in the Actions column.

            On the Device Details page, click the **Thing Model Data** \> **Events** tab to view the event details.

            ![Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5596789851/p38801.png)


## Online device debugging

1.  In the left-side navigation pane of the [IoT Platform console](https://iot.console.aliyun.com/), choose **Maintenance** \> **Online Debug**. On the **Online Debug** page, select the required product and device.

    ![Online debugging](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5596789851/p38803.png)

2.  Retrieve device properties.

    After specifying the Debug Feature and Method parameters, click **Dispatch Command**. The current temperature 35 is displayed in the editor.

    ![Debug physical devices](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5596789851/p38804.png)

3.  Change device properties.

    Change the temperature to 40 and click **Dispatch Command**. Go to the Status tab to view the device temperature. The temperature is changed to 40.

    ![Change device properties](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5596789851/p38805.png)

4.  If you debug user-defined device services, the system will print the relevant information to driver logs and return the following message:

    ```
    {"code":0,"message":"success"}
    ```


