---
keyword: data filtering
---

# Filter data that devices submit to Alibaba Cloud

This topic describes how to filter data that a device submits to Alibaba Cloud. In this example, a LightSensor device is specified.

-   An edge instance is created. For more information about how to create an edge instance, see [Build environments for Link IoT Edge Pro Edition](/intl.en-US/User Guide/Set up environments/Link IoT Edge Pro Edition/Install Link IoT Edge on Ubuntu 16.04.md) or [Build environments for Link IoT Edge Standard Edition](/intl.en-US/User Guide/Set up environments/Link IoT Edge Standard Edition/Install Link IoT Edge on Ubuntu 16.04.md).
-   A LightSensor device is created and assigned to the edge instance. For more information about how to create the LightSensor product and device, see [Sample drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Sample drivers.md).

Sensors constantly submit collected data. For example, a thermometer submits temperature values and a light sensor submits illuminance values. No significant difference exists in data that a device submits. Therefore, users only need to focus on the data that exceeds the limits. Link IoT Edge provides Function Compute-based edge applications to filter data that is submitted to Alibaba Cloud and reduce costs for using Alibaba Cloud resources.

Before using Function Compute-based edge applications to process data, you can view device data in the [IoT Platform console](http://iot.console.aliyun.com/). In the left-side navigation pane, choose **Devices** \> **Devices**. Find the required LightSensor device and click **View** in the Actions column. On the **Device Details** page, click the **Status** tab to view the device status.

![View device data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6839128851/p39090.png)

To view device data, click **View Data**. You can see that values change regularly from 100 to 600 with a difference ±100. Data is submitted every two seconds. Submitting data with a high frequency for a long term may incur unnecessary costs. You can use Function Compute-based edge applications to filter data that the device submits to Alibaba Cloud.

## 1. Create a data filtering function

1.  Download the following package of the data filtering function. You can use the function to filter illuminance values that the LightSensor device submits. For example, only the illuminance values that are greater than 500 or less than 200 can be submitted to Alibaba Cloud.

    [deviceDataFilter.zip](http://link-iot-edge-packet.oss-cn-shanghai.aliyuncs.com/fc-demo/deviceDataFilter.zip)

2.  Log on to the Alibaba Cloud [Function Compute console](https://fc.console.aliyun.com/).

    If you have not activated the Function Compute service, read the terms, select **I have read and agree**, and click **Activate Now**.

3.  Optional. In the left-side navigation pane, select **Service-Function**. From the drop-down list of **Create Function**, select **Create Service**. On the **Create Service** page, configure parameters and click **Create**.

    The **Service Name** parameter is required. In this example, you must specify EdgeFC for the Service Name parameter. You can specify other parameters based on your needs.

    **Note:** If the EdgeFC service has been created for other scenarios or applications, you do not need to create a new one.

4.  After creating the service, you must create a function. On the Service-Function page, click **Create Function**. On the **Create Function** page, select **Event Function** and click **Next**.

5.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |Service Name|Select EdgeFC.|
    |Function Name|Enter lightSensorDataFilter.|
    |Runtime|Configure the runtime environment for the function. In this example, select nodejs8.|
    |Function Handler|Use the default value `index.handler`.|
    |Memory|Select 512 MB.|
    |Timeout|Enter 10. Unit: seconds.|
    |Single Instance Concurrency|Use the default value.|

    You can configure other parameters based on your needs or leave them empty. For more information about how to configure parameters, see [Function Compute](https://www.alibabacloud.com/help/product/50980.htm).

    Confirm the function parameters and click **Create**.

6.  After the function is created, the function details page appears. On the **Code** tab, select **Upload Zip File** and click **Select File** to upload the [deviceDataFilter.zip](http://link-iot-edge-packet.oss-cn-shanghai.aliyuncs.com/fc-demo/deviceDataFilter.zip) package that you downloaded in step 1. Then, click **Save**.

    After the package is uploaded, you can view the source code on the **In-line Edit** tab.

    **Note:** You can also click the function name on the Service-Function page to go to the function details page, and click the **Code** tab to view the source code.

    ![The In-line Edit tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6839128851/p39287.png)

    **Note:** The lightSensorDataFilter sample code includes the following three operations.

    1.  Parse illuminance values from the data that the device submits. The event parameter is used to send data.

        ```
        var illuminance = iotData.getThingPropertyByEvent(event, "MeasuredIlluminance");
        ```

    2.  Check whether data meets filtering conditions.

        ```
        
        if (illuminance > 500 || illuminance < 200)
        ```

    3.  Submit data that meets the specified conditions.

        ```
        iotData.publish(message, (err, data)=> {callback(err);});
        ```

7.  Optional. Modify the data filtering conditions.

    After creating the function, you can edit the code to modify the data filtering conditions.

    The sample code provides the following default conditions to filter data. After you assign the function to the edge instance and deploy the instance, only illuminance values that are greater than 500 or less than 200 are submitted. To view submitted data, you can go to the **Device Details** page and click the **Status** tab.

    ```
    if (illuminance > 500 || illuminance < 200)
    ```

    You can modify the data filtering conditions. For example, if you specify the following condition, only illuminance values that are greater than 450 are submitted after you assign the function to the edge instance and deploy the instance. To view submitted data, you can go to the **Device Details** page and click the **Status** tab.

    ```
    if (illuminance > 450)
    ```


## 2. Assign the function to the edge instance

1.  In the left-side navigation pane of the [IoT Platform console](http://iot.console.aliyun.com/), choose **Link IoT Edge** \> **Applications**.

2.  Create a Function Compute-based edge application from the function that is created in step 1. For more information about how to create a Function Compute-based edge application, see [Use Function Compute to create edge applications](/intl.en-US/User Guide/Edge applications/Create edge applications/Use Function Compute to create edge applications.md).

    The following table describes the application parameters.

    |Parameter|Description|
    |---------|-----------|
    |Application Name|The name of the application. Example: lightSensorDataFilter.|
    |Application Type|Select Function Compute.|
    |Region|Select the region where the service is deployed.|
    |Service|Select **EdgeFC**.|
    |Function|Select **lightSensorDataFilter**.|
    |Authorization|Select **AliyunIOTAccessingFCRole**.|
    |Application Version|The version of the application. You must specify a unique version number.|

    The following table describes the function parameters.

    |Parameter|Description|
    |---------|-----------|
    |Running Mode|Two running modes are available. In this example, select **Continuous**. The application runs immediately after being deployed.|
    |Memory Limit \(MB\)|The maximum memory that is available for running the function. Unit: MB. Enter 512. If the memory that is used by the function exceeds the limit, the edge application is forced to restart.|
    |Timeout Limit \(Seconds\)|The maximum processing period after the function receives an event. Use the default value 5. If the function does not return the result within the specified period, the edge application is forced to restart.|
    |Scheduled Execution|Use the default value Close.|

    You do not need to specify other parameters.

3.  In the left-side navigation pane, choose **Link IoT Edge** \> **Edge Instances**.

4.  Find the created edge instance and click **View**.

5.  On the Instance Details page, click the **Edge Applications** tab. On this tab, click **Allocate Application**.

6.  Assign the **lightSensorDataFilter** function to the edge instance, and click **Close**.


## 5. Configure message routing

For more information about how to add a message route and specify parameters, see [Configure message routing](/intl.en-US/User Guide/Message routing/Configure message routing.md).

1.  On the Instance Details page, click the **Message Routing** tab. On this tab, remove the message route from the device to IoT Hub.

    **Note:** You must remove the message route that is configured when you created and assigned the LightSensor device to the edge instance. For information about how to create and assign devices to edge instance, see [Sample drivers](/intl.en-US/User Guide/Connect devices to Link IoT Edge/Sample drivers.md).

    ![Remove the message route](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7839128851/p39306.png)

2.  Click **Assign Route** to add a message route from the LightSenor device to Function Compute.

    Specify the following parameters based on prompted instructions and click **OK** to add the first message route.

    |Parameter|Description|
    |---------|-----------|
    |Route Name|The name of the message route.|
    |Message Source|Select **Device** and choose **LightSensor** \> **LightSensor**.|
    |Message Topic Filter|Select **All**.|
    |Message Destination|Select **Function Compute**. Then, select **EdgeFC/LightSensorDataFilter**.|

3.  On the Instance Details page, click the **Devices & Drivers** tab. Find the LightSensor device and click **View** to go to the **Device Details** page.

4.  Click the **Topic List** tab. On this tab, select**Custom Topics**. In the Device Topic column, copy the first entry.

    ![Query the topic list of the device](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7839128851/p39307.png)

5.  Go to the Instance Details page, and click **Assign Route** to add a message route from Function Compute to IoT Hub.

    Specify the following parameters based on prompted instructions and click **OK** to add the second message route.

    |Parameter|Description|
    |---------|-----------|
    |Route Name|The name of the message route.|
    |Message Source|Select **Function Compute**. Then, select **EdgeFC/LightSensorDataFilter**.|
    |Message Topic Filter|Enter the topic that you copied in the previous step.|
    |Message Destination|Select **IoT Hub**.|
    |Service level|Select **0**.|


## 4. Deploy the edge instance

1.  On the Instance Details page, click **Deploy** in the upper right corner. In the dialog box that appears, click **OK** to assign resources such as sub-devices and Function Compute-based edge applications to the edge instance.

    You can click **Deployment Details** to view the deployment progress and result.

2.  Optional. On the **Instance Details** page, click the **Monitoring** tab. On this tab, select **Edge Applications** to view monitoring data of the Function Compute-based edge application that is assigned to the edge instance.

    Find the required application and click **View** in the Actions column to view monitoring details.

    ![View monitoring data of Function Compute](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7839128851/p55764.png)

3.  On the Instance Details page, click the **Devices & Drivers** tab. Find the LightSensor device and click **View** to go to the **Device Details** page.

    On the Device Details page, click Status to view the data of the LightSensor device.

    ![View device data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7839128851/p39308.png)

    You have completed the procedure of using a Function Compute-based edge application to filter data that a device submits to Alibaba Cloud.


