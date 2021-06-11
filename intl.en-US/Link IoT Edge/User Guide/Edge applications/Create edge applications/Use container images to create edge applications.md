---
keyword: [Edge applications, Create edge applications based on container images]
---

# Use container images to create edge applications

This topic describes how to use container images to create edge applications.

-   The [Alibaba Cloud Container Registry](https://www.alibabacloud.com/help/product/60716.htm) service is activated.
-   An image is created if you want to use an image from a private image repository in Container Registry to create the edge application. For more information, see the [Container Registry documentation](https://www.alibabacloud.com/help/product/60716.htm).

1.  Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list).

2.  On the Applications page, click **Create Application**.

3.  On the page that appears, specify the parameters as prompted and click **Confirm**.

    -   Application Information

        ![Container image (application information)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2349128851/p65629.png)

        |Parameter|Description|
        |---------|-----------|
        |Application Name|The name of the edge application. The application name must be 1 to 128 characters in length, and can contain letters, digits, and underscores \(\_\).|
        |Application Type|The method that is used to create the edge application. The valid values are described as follows:         -   Function Compute: This value indicates that the edge application is created by using [Function Compute](https://www.alibabacloud.com/help/product/50980.htm).
        -   Container Image: This value indicates that the edge application is created by using [Container Registry](https://www.alibabacloud.com/help/product/60716.htm).
        -   Local Upload: This value indicates that the edge application is created by using locally developed functions.
In this example, select Container Image. |
        |Repository Type|The type of the image repository. The valid values are described as follows:         -   Public Repository: An image from a public image repository is used to create the edge application.
        -   Alibaba Cloud Container Registry: An image from a private image repository in Container Registry is used to create the edge application. |
        |Image Address|The download URL of the public image. This parameter is available only when you set Repository Type to Public Repository. You must enter a URL where the image tag is specified. The valid format is described as follows: `mysql:latest`.|
        |Select Region|The region where your private image repository resides. This parameter is available only when you set Repository Type to Alibaba Cloud Image Repository. You must select the region where your private image repository resides.|
        |Namespace|The namespace. This parameter is available only when you set Repository Type to Alibaba Cloud Image Repository. You must select the namespace where your private image repository resides.|
        |Image Repository|The private image repository. This parameter is available only when you set Repository Type to Alibaba Cloud Image Repository. You must select your private image repository.|
        |Image Version|The version of the image. This parameter is available only when you set Repository Type to Alibaba Cloud Image Repository. You must select the version of the image that is stored in your private image repository.|
        |Application Version|The version number of the edge application. You cannot specify two identical version numbers for an edge application.|
        |Version Description|The description of the edge application version. For example, you can specify the version features and purposes. This parameter is optional.|
        |Environment Variables|The custom environment variables. The system can read the specified environment variables when you run the code of the Function Compute-based edge application. To add an environment variable, click **Add Environment Variable**. Then, specify the variable name and variable value. You can add a maximum of 10 environment variables.|

    -   Container Configurations

        ![Container image (container configurations)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3349128851/p65630.png)

        |Parameter|Description|
        |---------|-----------|
        |Entrypoint|Optional. The entry point. The specified string cannot exceed 128 bytes in length. The command that is specified by this parameter is the first command that the container runs after the container is started.|
        |Command Line Parameters \(CMD\)|Optional. The command line parameters. You can specify the command line parameters for the entry point. A maximum of 10 parameters can be specified, and each string cannot exceed 128 bytes in length. For example, if you want to run 1,000 ping commands to test the connection between the container and the aliyun.com web page, you can run the `ping aliyun.com -c 1000` command. In this example, set the parameters as follows:

        -   Entrypoint=ping
        -   First command line parameter=aliyun.com
        -   Second command line parameter=-c
        -   Third command line parameter=1000 |
        |Host Mode|Specifies whether to isolate the container network from the host network. The valid values are described as follows:         -   Yes: This value indicates that the container network is the same as the host network.
        -   No: This value indicates that the container network is isolated from the host network. If you select this option, you must configure the Network Port Mapping settings. |
        |Network Port Mapping|The mappings between host network ports and container network ports. This parameter is available only when you select No for Host Mode. The network where the function runs is isolated from the host network. You can map the listening port of the function in the container to a host network port. This allows client programs on various hosts to access the services that are provided by the function. You can specify a maximum of 10 entries. For example, the `fc-http-server` function runs in a host container, and provides services by using socket port 80. The client programs on other hosts cannot access the `fc-http-server` function by accessing port 80 on the current host. To enable the client programs on other hosts to access the `fc-http-server` function, you must map the network port \(port 80\) in the container where the function runs to a host network port, such as port 8080. Then, the client programs on other hosts can access the `IP address:port 8080` in the host network, and use the services provided by the `fc-http-server` function. |
        |Privilege Mode|Specifies whether to enable the privilege mode. Root users of containers can access host services only as general users. If you want to change the system time or run the mount command in containers, you must be granted the required root permissions. In this scenario, you must enable the privilege mode for the containers. **Note:** If you enable the privilege mode, applications and programs in the containers are granted the host root permissions, and all the host devices are mapped to the containers. Therefore, you do not need to configure the Device Mapping settings. |
        |Device Mapping|The device mappings. This parameter is available only when you select No for Privilege Mode. The network where the device management system resides is isolated from the host network. To enable a function to access a host device such as a serial interface, you must map the device to the container where the function runs. You can specify a maximum of 10 entries.|
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

