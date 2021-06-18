# Publish built-in drivers

Link IoT Edge allows you to deploy built-in drivers to your gateway. This feature allows you to manage the on-premises driver files, configure the drivers on the cloud, and then deploy the drivers to the edge.

A built-in driver that complies with the driver specifications of Link IoT Edge. For more information, see [Driver development](/intl.en-US/Link IoT Edge/User Guide/Connect devices to Link IoT Edge/Develop drivers/Overview.md).

IoT Link Edge supports the use of built-in drivers. You can upload the built-in drivers to your gateway and configure the driver information \(such as the driver name, coding language, runtime environment, and hardware architecture\) on the cloud. You can then configure the driver channel and device on the cloud.

![Publish built-in drivers](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1349128851/p86374.png)

The following figure shows the process of publishing a built-in driver.

![The flowchart for publishing a built-in driver](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1349128851/p86617.png)

## 1. Procedure on the cloud

1.  Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). In the left-side navigation pane, click **Drivers**.

2.  On the Drivers page, click the Custom Drivers tab. On the Custom Drivers tab, click **Create Driver**.

3.  On the **Create Driver**page, specify the parameters as prompted.

    -   Driver Information

        ![Publish built-in drivers](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1349128851/p89053.png)

        |Parameter|Description|
        |---------|-----------|
        |Driver Name|The name of the custom driver. The name must be 1 to 20 characters in length, and can contain letters, digits, and underscores \(\_\). The name must start with a letter.|
        |Communication Protocol|The communication protocol that is used to develop the driver. Valid values: Modbus, OPCUA, and Custom.|
        |Language|The programming language that is used to develop the driver. Valid values: Node.js 8, Python 3.5, C, and Java 8. If you set the Language parameter to C, you must set the CPU Architecture parameter. |
        |Built-in Driver|Specifies whether the driver is built-in.         -   If you select Yes, a local built-in driver is used. You do not need to upload a driver file.
        -   If you select No, you must upload a driver file and deploy the driver to the cloud. For more information, see [Publish drivers to the cloud](/intl.en-US/Link IoT Edge/User Guide/Connect devices to Link IoT Edge/Publish drivers/Publish cloud-hosted drivers.md).
To publish a built-in driver, you must select Yes. |
        |Driver Version|The unique version number of the driver. You cannot specify two identical version numbers for a driver.|
        |Link IoT Edge Version for the Driver|The Link IoT Edge version that supports the driver. The driver can run only in the gateways for Link IoT Edge of the specified version or later.|
        |Version Description|Optional. The description of the driver version.|

    -   Driver Configurations

        ![Publish drivers to the cloud (driver configurations)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2495328851/p73189.png)

        |Parameter|Description|
        |---------|-----------|
        |Configuration Format|The configuration method. Valid values:         -   Key-value Configuration
        -   JSON Format
        -   Configuration File |
        |Configuration Format: Key-value Configuration|If you select Key-value Configuration, click **Add Configuration**. Then, set the Configuration Name, Value, and Description parameters to configure the driver. You can add a maximum of 100 key-value pairs. |
        |Configuration Format: JSON Format|If you select JSON Format, enter JSON-formatted data to configure the driver. The data size cannot exceed 1 KB. Link IoT Edge automatically verifies the format. If the format is invalid, modify the JSON-formatted data as prompted.|
        |Configuration Format: Configuration File|If you select Configuration File, edit a configuration file on your computer and upload it to the Link IoT Edge console.|

    -   Container Configurations

        ![Publish drivers to the cloud (container configurations)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2495328851/p73204.png)

        |Parameter|Description|
        |---------|-----------|
        |Host Mode|Specifies whether to isolate the container network from the host network. Valid values:         -   Yes: The container network is the same as the host network.
        -   No: The container network is isolated from the host network. If you select this option, you must set the Network Port Mapping parameter. |
        |Network Port Mapping|The mappings between host network ports and container network ports. This parameter is available only when you set the Host Mode parameter to No. The network where the function runs is isolated from the host network. You can map the listening port of the function in the container to a host network port. This allows client programs on various hosts to access the services that are provided by the function. You can specify a maximum of 10 entries. For example, the `fc-http-server` function runs in a host container, and provides services by using Port 80. The client programs on other hosts cannot access the `fc-http-server` function by accessing Port 80 on the current host. To enable the client programs on other hosts to access the `fc-http-server` function, you must map Port 80 in the container where the function runs to a host network port, such as Port 8080. Then, the client programs on other hosts can access `IP address:port 8080` on the host network, and use the services provided by the `fc-http-server` function. |
        |Privilege Mode|Specifies whether to enable the privilege mode. Root users of containers can access host services only as regular users. If you need to change the system time or run the mount command in containers, you must be granted the required root permissions. In this scenario, you must enable the privilege mode for the containers.

**Note:** If you enable the privilege mode, applications and programs in the containers are granted the host root permissions, and all the host devices are mapped to the containers. Therefore, you do not need to set the Device Mapping parameter. |
        |Device Mapping|The device mappings. This parameter is available only when you set the Privilege Mode parameter to No. The network where the device management system resides is isolated from the host network. To enable a function to access a host device such as a serial port, you must map the device to the container where the function runs. You can specify a maximum of 10 entries.|
        |Volume Mapping|The volume mappings. The network where the file system resides is isolated from the host network. To enable a function to access a host file, you must map the file to the container where the function runs. You can specify a maximum of 10 entries.|

    -   Configuration Verification

        ![Configuration Verification](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2495328851/p73214.png)

        |Parameter|Description|
        |---------|-----------|
        |Driver Configurations|If you select **Driver Configurations**, you must complete driver configurations before you can deploy the edge instance. The driver configurations are specified after the driver is assigned to an edge instance and sub-devices are assigned to the driver.|
        |Device Configurations|If you select **Device Configurations**, you must complete device configurations before you can deploy the edge instance. The device configurations are specified after the driver is assigned to an edge instance and sub-devices are assigned to the driver.|

4.  After the parameters are set, click **Confirm**. You can find the driver that has been created on the Custom Drivers tab.

    ![Driver ID](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2349128851/p89085.png)

    You can move the pointer over the driver name to view the driver ID. Click **Copy** and save the driver ID, which will be used in subsequent steps.


## 2. Procedure at the edge

Link IoT Edge provides the led\_driver sample driver. For more information, visit [led\_driver source code](https://github.com/aliyun/linkedge-thing-access-sdk-c/tree/master/demo). You can use the sample driver for testing and debugging.

1.  Create an edge instance and connect the edge gateway to IoT Platform. For more information, see [Set up environments](/intl.en-US/Link IoT Edge/User Guide/Set up environments/Link IoT Edge Pro Edition/Install Link IoT Edge on Ubuntu 16.04.md).

2.  Log on to the gateway and run the following command to create a driver directory:

    ```
    sudo -E mkdir -p /linkedge/pre-installed/
    ```

3.  Run the following command to create a folder with built-in drivers. Save the driver files and dependent libraries that you have prepared in the Prerequisites section to this folder.

    ```
    sudo -E mkdir -p /linkedge/pre-installed/{your_driver_name}/
    ```

    \{your\_driver\_name\} is the name of your driver. For example, if the driver name is led\_driver, the actual command is as follows:

    ```
    sudo -E mkdir -p /linkedge/pre-installed/led_driver/
    ```

4.  Check whether the following tools for built-in driver are installed on the gateway.

    |Tool|Function|
    |----|--------|
    |sed|Finds and replaces the contents of text files.|
    |jq|Parses JSON files.|
    |base64|Provides Base64 encryption.|

5.  Optional. If the gateway does not have tools such as sed, jq, or base64, you must perform the following steps to ensure that the shell script tool for the built-in driver runs normally:

    1.  Go to the default configuration directory of Link IoT Edge.

        ```
        cd /linkedge/gateway/build/config/config-manager
        ```

    2.  Open the config\_default.json file, and find the config parameter.

    3.  Under config, add the following `key: value` pair:

        ```
        {
            "config": {
                "gw_drivercode_\{your\_driver\_id\}": "\{your\_driver\_path\}",
            }
        }
        ```

        \{your\_driver\_id\} is the driver ID that you copied in the [1. Procedure on the cloud](#section_dmk_h1u_tmj) section. \{your\_driver\_path\} is the built-in driver folder path after Base64 encryption.

        In the following example, the driver ID is f16f13322\*\*\*\*\*\*\*\*\*\*\*3959 cf3, the path of the built-in driver folder is /linkedge/pre-installed/led\_driver/, and the Base64-encrypted path is L2xpbmtlZGdlL3ByZS1pbnN0YWxsZWQvbGVkX2RyaXZlcg==. Then the correct `key: value` pair is as follows:

        ```
        {
            "config": {
                "gw_drivercode_f16f133222************3959cf3": "L2xpbmtlZGdlL3ByZS1pbnN0YWxsZWQvbGVkX2RyaXZlcg==",
            }
        }
        ```

6.  In the built-in driver folder, download and decompress the [shell script tool for built-in drivers](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/testingTool/pre-installed.tar.gz).

    The following code shows the directory structure of the script tool after decompression.

    ```
    .
    └-- led_driver
        |-- pre-installed.sh
        |-- lib
        └-- main
    ```

7.  Go to the directory where the built-in driver is located and run the shell script tool.

    ```
    cd /linkedge/pre-installed/{your_driver_name}/
    sudo -E ./pre-installed.sh {your_driver_id} --default
    ```

    \{your\_driver\_name\} is the driver name and \{your\_driver\_id\} is the driver ID that you saved in the [1. Procedure on the cloud](#section_dmk_h1u_tmj) section.

    For example, if the driver name is led\_driver and the driver ID is f16f13322\*\*\*\*\*\*\*\*\*\*\*3959 cf3, the actual command is as follows:

    ```
    cd /linkedge/pre-installed/led_driver/
    sudo -E ./pre-installed.sh f16f13322**********3959cf3
    ```

8.  Assign the built-in driver to the edge instance and deploy the edge instance to complete the process of publishing the build-in driver. For more information, see [Debug drivers](/intl.en-US/Link IoT Edge/User Guide/Connect devices to Link IoT Edge/Develop drivers/Debug drivers.md).


## FAQ

Q: Why does my devices not come online after I run the shell script?

A: You must finish the driver configuration on the cloud and deploy the driver to the gateway before the associated sub-devices can come online.

1.  Log on to the [IoT Platform console](https://iot.console.aliyun.com/). In the left-side navigation pane, choose **Link IoT Edge** \> **Drivers**.
2.  On the Custom Drivers tab of the **Drivers** page, click **Version Management** in the Actions column.

    ![Driver version management](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2495328851/p76055.png)

3.  On the **Version Management** page, you can manage the driver versions. The following table lists the available operations.

    |Operation|Description|
    |---------|-----------|
    |Create Version|You can click **Create Version** to create a new version of the driver. For parameter configurations, see the [1. Procedure on the cloud](#section_dmk_h1u_tmj) section of in this topic.|
    |Publish|You can click **Publish** to publish the specified version. In the **Publish Driver** dialog box, confirm the driver information, and click **Publish**. **Note:** After the version of the driver is published, you cannot Delete the version of the driver. You can only View the version details or Download the version of the driver. |
    |Edit|You can edit the driver configurations only when the driver version is in the Unpublished state. Click **Edit** to edit the driver configurations. For more information, see the [1. Procedure on the cloud](#section_dmk_h1u_tmj) section of this topic.|
    |Download|You can click **Download** to download the specified version of the driver.|
    |Delete|You can delete a driver version only when the driver version is in the Unpublished state. You can click **Delete** to delete the specified version of the driver.|
    |View|You can view the driver version details only when the driver version is in the Published state. Click **View** to view the driver version details or modify the configurations of the driver version. For more information, see the [1. Procedure on the cloud](#section_dmk_h1u_tmj) section of this topic.|

4.  After you publish the driver on the cloud, you can assign the driver to an edge instance and assign sub-devices to the driver. Then, you can deploy the driver and its sub-devices to the edge by deploying the edge instance. For more information, see [Debug drivers](/intl.en-US/Link IoT Edge/User Guide/Connect devices to Link IoT Edge/Develop drivers/Debug drivers.md).

