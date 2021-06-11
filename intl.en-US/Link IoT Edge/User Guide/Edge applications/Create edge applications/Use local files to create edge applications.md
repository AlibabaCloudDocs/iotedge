---
keyword: [Edge applications, Create edge applications based on local files]
---

# Use local files to create edge applications

This topic describes how to use local files to create edge applications.

A function is locally created. For more information, see [Function Compute Guide](https://www.alibabacloud.com/help/doc-detail/75152.htm).

1.  Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list).

2.  On the Applications page, click **Create Application**.

3.  On the page that appears, specify the parameters as prompted and click **Confirm**.

    -   Application Information

        ![Edge applications that are created based on local files (application information)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5349128851/p65650.png)

        |Parameter|Description|
        |---------|-----------|
        |Application Name|The name of the edge application. The application name must be 1 to 128 characters in length, and can contain letters, digits, and underscores \(\_\).|
        |Application Type|The method that is used to create the edge application. The valid values are described as follows:         -   Function Compute: This value indicates that the edge application is created by using [Function Compute](https://www.alibabacloud.com/help/product/50980.htm).
        -   Container Image: This value indicates that the edge application is created by using [Container Registry](https://www.alibabacloud.com/help/product/60716.htm).
        -   Local Upload: This value indicates that the edge application is created by using locally developed functions.
In this example, select Local Upload. |
        |Programming Language|The programming language that you use to develop the function. The supported programming languages are Node.js, Python, and C. **Note:** The functions that are created by using the Python programming language can be used only in edge instances of Link IoT Edge Pro Edition. |
        |Application Version|The version number of the edge application. You cannot specify two identical version numbers for an edge application.|
        |Code Package|The code file that you want to upload. To upload the code file that is locally created, click **Upload File**. **Note:** You can upload only a file that is in the .zip file format. |
        |Version Description|The description of the edge application version. For example, you can specify the version features. This parameter is optional.|

    -   Container Configurations

        **Note:**

        |Parameter|Description|
        |---------|-----------|
        |Host Mode|Specifies whether to isolate the container network from the host network. Valid values:         -   Yes: The container network is the same as the host network.
        -   No: The container network is isolated from the host network. If you select this option, you must set the Network Port Mapping parameter. |
        |Network Port Mapping|The mappings between host network ports and container network ports. This parameter is available only when you set the Host Mode parameter to No. The network where the function runs is isolated from the host network. You can map the listening port of the function in the container to a host network port. This allows client programs on various hosts to access the services that are provided by the function. You can specify a maximum of 10 entries. For example, the `fc-http-server` function runs in a host container, and provides services by using Port 80. The client programs on other hosts cannot access the `fc-http-server` function by accessing Port 80 on the current host. To enable the client programs on other hosts to access the `fc-http-server` function, you must map Port 80 in the container where the function runs to a host network port, such as Port 8080. Then, the client programs on other hosts can access `IP address:port 8080` on the host network, and use the services provided by the `fc-http-server` function. |
        |Privilege Mode|Specifies whether to enable the privilege mode. Root users of containers can access host services only as regular users. If you need to change the system time or run the mount command in containers, you must be granted the required root permissions. In this scenario, you must enable the privilege mode for the containers.

**Note:** If you enable the privilege mode, applications and programs in the containers are granted the host root permissions, and all the host devices are mapped to the containers. Therefore, you do not need to set the Device Mapping parameter. |
        |Device Mapping|The device mappings. This parameter is available only when you set the Privilege Mode parameter to No. The network where the device management system resides is isolated from the host network. To enable a function to access a host device such as a serial port, you must map the device to the container where the function runs. You can specify a maximum of 10 entries.|
        |Volume Mapping|The volume mappings. The network where the file system resides is isolated from the host network. To enable a function to access a host file, you must map the file to the container where the function runs. You can specify a maximum of 10 entries.|

4.  View the edge application that you created on the **Applications** page. You can also click buttons in the Actions column to manage the edge application.

    ![Manage the edge application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5349128851/p65548.png)

    -   Manage versions

        To manage versions, click **Version Management**. In the Version Management panel, you can create, modify, or delete versions based on your business requirements.

        ![Application version management](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5349128851/p65550.png)

    -   Delete the edge application

        To delete the edge application, click **Delete**.

        **Note:** Before you delete the edge application, you must delete all versions of the edge application. Otherwise, the edge application cannot be deleted.


You can assign the edge application that has been created to the edge instance. For more information, see [Assign edge applications to edge instances](/intl.en-US/Link IoT Edge/User Guide/Edge applications/Assign edge applications to edge instances.md).

