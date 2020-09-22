# invokeFunction

调用该接口，调用指定的函数。

## 说明

调用函数和[发布消息](/cn.zh-CN/边缘端开发指南/函数计算SDK/Nodejs/Publish.md)，两者都可以在进程（函数）间传递消息，但区别是：

-   函数调用消息是双向的。调用者发送消息给被调用者后，会收到被调用者处理后返回的消息。
-   发布消息是单向的。发送者不需要被调用者的返回信息。

## invokeFunction\(params, callback\)

|参数|类型|描述|
|:-|:-|:-|
|params|object|参数对象。需包含的必需参数，请参见表[params参数说明](#params)。|
|callback\(err, data\)|function|回调函数。遵循JavaScript标准实践。具体请参见表[callback参数说明](#callback)。|

|参数|类型|描述|
|:-|:-|:-|
|serviceName|String|服务名。函数在[阿里云函数计算](https://www.aliyun.com/product/fc)中所属服务的名称。|
|functionName|String|函数名，在[阿里云函数计算](https://www.aliyun.com/product/fc)中设置的函数名。|
|invocationType|String|调用类型。 -   Sync：同步调用。
-   Async：异步调用。

 默认为同步调用。|
|payload|String\|Buffer|参数信息作为函数的输入。|

|参数|类型|描述|
|:-|:-|:-|
|err|Error|-   调用成功，err为null。
-   调用失败，err包含发生的错误信息。 |
|data|object|被调函数的返回值。|

## 调用示例

-   调用者函数代码示例

    在Invoker中，调用serviceName=EdgeFC， functionName=helloworld的函数。

    ```
    'use strict';
    
    const leSdk = require('linkedge-core-sdk');
    const fc = new leSdk.FCClient();
    
    module.exports.handler = function (event, context, callback) {
      var ctx = {
        custom: {
          data: 'Custom context from Invoker',
        },
      };
      var invokerContext = Buffer.from(JSON.stringify(ctx)).toString('base64');
      var invokeParams = {
        serviceName: 'EdgeFC',
        functionName: 'helloworld',
        invocationType: 'Sync',
        invokerContext: invokerContext,
        payload: 'String message from Invoker.',
      };
      fc.invokeFunction(invokeParams, (err, data) => {
        if (err) {
          console.log(err);
        } else {
          console.log(data.payload); // Message from helloworld
        }
        callback(null);
      });
    };
    ```

-   被调用函数代码示例

    以下helloworld函数代码表示被调用函数如何解析调用者传入的参数，以及如何返回结果给调用者。

    ```
    module.exports.handler = function(event, context, callback) {
      console.log(event);   // String message from Invoker.
      console.log(context); // { requestId: '4', invokerContext: {custom: { data: 'Custom data from Invoker' }}}
      console.log(context.invokerContext.custom.data); // Custom data from Invoker
      console.log('-- hello world');
      callback(null, 'Message from helloworld'); // Return the result to Invoker.
    };
    ```


