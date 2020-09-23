# invokeFunction

调用该接口，调用指定的函数。

## 说明

调用函数和[发布消息](/cn.zh-CN/边缘端开发指南/函数计算SDK/Python/publish.md)，两者都可以在进程（函数）间传递消息，但区别是：

-   函数调用消息是双向的。调用者发送消息给被调用者后，会收到被调用者处理后返回的消息。
-   发布消息是单向的。发送者不需要被调用者的返回信息。

## invokeFunction\(params\)

|参数|类型|描述|
|:-|:-|:-|
|params|dict|参数对象。需包含的必需参数，请参见表[params参数说明](#params)。|

|参数|类型|描述|
|:-|:-|:-|
|serviceName|String|服务名。函数在[阿里云函数计算](https://www.aliyun.com/product/fc)中所属服务的名称。|
|functionName|String|函数名，在[阿里云函数计算](https://www.aliyun.com/product/fc)中设置的函数名。|
|invocationType|String|调用类型。-   Sync：同步调用。
-   Async：异步调用。

默认为同步调用。|
|payload|String\|Bytes|参数信息作为函数的输入。|

|参数|类型|描述|
|:-|:-|:-|
|return|dict|被调用函数的返回值。|

## 调用示例

-   **调用者函数代码示例**

    在Invoker中，调用serviceName=EdgeFC，functionName=helloworld的函数。

    ```
    # -*- coding: utf-8 -*-
    import lecoresdk
    edgefc = lecoresdk.Client()
    
    def handler(event, context):
      context = {"custom": {"data": "customData"}}
      invokeParams = {
        "serviceName": 'EdgeFC',
        "functionName": 'helloworld',
        "invocationType": 'Sync',
        "invokerContext": context,
        "payload": 'String message from Python Invoker.'
      };
      res = edgefc.invoke_function(invokeParams)
      print(res)
      return 'OK'
    ```

-   **被调用函数代码示例**

    以下helloworld函数代码表示被调用函数如何解析调用者传入的参数，以及如何返回结果给调用者。

    ```
    # -*- coding: utf-8 -*-
    import logging
    import lecoresdk
    
    def handler(event, context):
      logging.debug(event)
      logging.debug(context)
      return 'hello world'
    ```


