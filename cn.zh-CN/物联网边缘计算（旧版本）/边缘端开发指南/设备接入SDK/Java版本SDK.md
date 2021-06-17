# Java版本SDK

设备接入SDK（Java版本）支持开发者使用Java语言开发设备接入驱动（以下简称驱动）。客户网关环境在安装有Link IoT Edge软件的条件下只要满足Java运行环境即可运行Java驱动。

Java版本SDK的源码以及使用示例，请参见[开源Java库](https://github.com/aliyun/linkedge-thing-access-sdk-java)。

## LedaConfig

-   类名全称：`com.aliyun.linkedge.sdk.LedaConfig`
-   类声明：

    ```
    public class LedaConfig
    ```

-   Java方法说明：

    |限定符和类型|方法和说明|
    |------|-----|
    |static String|getDriverConfig\(\) 获取驱动配置。 |
    |static String|getDeviceConfig\(\) 获取设备配置。 |
    |static String|getTsl\(String productKey\) 获取productKey（产品唯一标识符）对应的物模型（TSL）。 |
    |static String|getTslConfig\(String productKey\) 获取productKey对应的物模型扩展配置。 |


## LedaDevice

-   类名全称：`com.aliyun.linkedge.sdk.LedaDevice`
-   类声明：

    ```
    public class LedaDevice
    ```

-   构造函数：

    ```
    LedaDevice(String productKey, String deviceName)
    ```

-   Java方法说明：

    |限定符和类型|方法和说明|
    |------|-----|
    |LedaData|getProperties\(List<String\> propertyNameList\) 根据指定的属性名称，获取属性值。使用该方法时，需要实现重载（Overload）。 |
    |int|setProperties\(HashMap<String, Object\> properties\) 设置属性名称和属性值。使用该方法时，需要实现重载。 |
    |LedaData|callService\(String methodName, HashMap<String, Object\> params\) 执行自定义方法。使用该方法时，需要实现重载。 |
    |int|online\(\) 上线设备。 |
    |int|offline\(\) 下线设备。 |
    |int|reportProperties\(HashMap<String, Object\> properties\) 上报设备属性。 |
    |int|reportEvents\(String eventName, HashMap<String, Object\> outputData\) 上报设备事件。 |


## 数据类

-   类名全称：`com.aliyun.linkedge.sdk.LedaDevice`
-   类声明：

    ```
    public class LedaData
    ```

-   构造函数：

    ```
    LedaData(int code, HashMap<String, Object> data)
    ```

-   Java方法说明：

    |限定符和类型|方法和说明|
    |------|-----|
    |void|setCode\(int code\) 设置状态码。 |
    |int|getCode\(\) 获取状态码。 |
    |void|setData\(HashMap<String, Object\> data\) 设置数据内容。 |
    |HashMap<String, Object\>|getData\(\) 获取数据内容。 |


## 错误码

-   类名全称：`com.aliyun.linkedge.sdk.exception.LedaErrorCode`
-   类声明：

    ```
    public class LedaErrorCode {
        public static final int LE_SUCCESS                              = 0;
        public static final int LE_ERROR_UNKNOWN                        = 100000;
        public static final int LE_ERROR_INVALID_PARAM                  = 100001;
        public static final int LE_ERROR_TIMEOUT                        = 100006;
        public static final int LE_ERROR_PARAM_RANGE_OVERFLOW           = 100007;
        public static final int LE_ERROR_SERVICE_UNREACHABLE            = 100008;
        public static final int LEDA_ERROR_DEVICE_UNREGISTER            = 109000;
        public static final int LEDA_ERROR_DEVICE_OFFLINE               = 109001;
        public static final int LEDA_ERROR_PROPERTY_NOT_EXIST           = 109002;
        public static final int LEDA_ERROR_PROPERTY_READ_ONLY           = 109003;
        public static final int LEDA_ERROR_PROPERTY_WRITE_ONLY          = 109004;
        public static final int LEDA_ERROR_SERVICE_NOT_EXIST            = 109005;
        public static final int LEDA_ERROR_SERVICE_INPUT_PARAM          = 109006;
        public static final int LEDA_ERROR_INVALID_JSON                 = 109007;
        public static final int LEDA_ERROR_INVALID_TYPE                 = 109008;
    
        private static final String LE_SUCCESS_MSG                      = "Success";                          /* 请求成功*/
        private static final String LE_ERROR_INVALID_PARAM_MSG          = "Invalid params";                   /* 传入参数为NULL或无效*/
        private static final String LE_ERROR_TIMEOUT_MSG                = "Tiemout";                          /* 超时*/
        private static final String LE_ERROR_PARAM_RANGE_OVERFLOW_MSG   = "Param range overflow";             /* 参数范围越界*/
        private static final String LE_ERROR_SERVICE_UNREACHABLE_MSG    = "Service unreachable";              /* 服务不可达*/
    
        private static final String LEDA_ERROR_DEVICE_UNREGISTER_MSG    = "Device has't register";            /* 设备未注册*/ 
        private static final String LEDA_ERROR_DEVICE_OFFLINE_MSG       = "Device has offline";               /* 设备已下线*/
        private static final String LEDA_ERROR_PROPERTY_NOT_EXIST_MSG   = "Property no exist";                /* 属性不存在*/
        private static final String LEDA_ERROR_PROPERTY_READ_ONLY_MSG   = "Property only support read";       /* 属性只读*/
        private static final String LEDA_ERROR_PROPERTY_WRITE_ONLY_MSG  = "Property only support write";      /* 属性只写*/
        private static final String LEDA_ERROR_SERVICE_NOT_EXIST_MSG    = "Service no exist";                 /* 服务不存在*/
        private static final String LEDA_ERROR_SERVICE_INPUT_PARAM_MSG  = "Service param invalid";            /* 服务的输入参数不正确错误码*/
        private static final String LEDA_ERROR_INVALID_JSON_MSG         = "Json format invalid";              /* JSON格式错误*/
        private static final String LEDA_ERROR_INVALID_TYPE_MSG         = "Param type invalid";               /* 参数类型错误*/
    }
    ```

-   Java方法说明：

    |限定符和类型|方法和说明|
    |------|-----|
    |String|getMessage\(int code\) 获取错误码对应的消息。 |


