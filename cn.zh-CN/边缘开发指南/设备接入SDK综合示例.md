# 设备接入SDK综合示例 {#concept_xjf_j2p_32b .concept}

本文展示一段使用设备接入SDK，开发驱动的代码片段。设备使用thing标识，拥有一个temperature的只读属性，在连接到边缘计算节点后，每隔2秒向平台上报属性和高温事件。

## Node.js版本 {#section_wlk_g52_h2b .section}

```
/*
 * Copyright (c) 2018 Alibaba Group Holding Ltd.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

'use strict';

const {
  RESULT_SUCCESS,
  RESULT_FAILURE,
  ThingAccessClient,
} = require('linkedge-thing-access-sdk');

var driverConfig;
try {
  driverConfig = JSON.parse(process.env.FC_DRIVER_CONFIG)
} catch (err) {
  throw new Error('The driver config is not in JSON format!');
}
var configs = driverConfig['deviceList'];
if (!Array.isArray(configs) || configs.length === 0) {
  throw new Error('No device is bound with the driver!');
}

var args = configs.map((config) => {
  var self = {
    config,
    thing: {
      temperature: 41,
    },
    callbacks: {
      setProperties: function (properties) {
        // Usually, in this callback we should set properties to the physical thing and
        // return the result. Here we just return a failed result since the properties
        // are read-only.
        console.log('Set properties %s to thing %s-%s', JSON.stringify(properties),
          config.productKey, config.deviceName);
        // Return an object representing the result in the following form or the promise
        // wrapper of the object.
        return {
          code: RESULT_FAILURE,
          message: 'failure',
        };
      },
      getProperties: function (keys) {
        // Usually, in this callback we should get properties from the physical thing and
        // return the result. Here we return the simulated properties.
        console.log('Get properties %s from thing %s-%s', JSON.stringify(keys),
          config.productKey, config.deviceName);
        // Return an object representing the result in the following form or the promise
        // wrapper of the object.
        if (keys.includes('temperature')) {
          return {
            code: RESULT_SUCCESS,
            message: 'success',
            params: {
              temperature: self.thing.temperature,
            }
          };
        }
        return {
          code: RESULT_FAILURE,
          message: 'The requested properties does not exist.',
        }
      },
      callService: function (name, args) {
        // Usually, in this callback we should call services on the physical thing and
        // return the result. Here we just return a failed result since no service
        // provided by the thing.
        console.log('Call service %s with %s on thing %s-%s', JSON.stringify(name),
          JSON.stringify(args), config.productKey, config.deviceName);
        // Return an object representing the result in the following form or the promise
        // wrapper of the object
        return new Promise((resolve) => {
          resolve({
            code: RESULT_FAILURE,
            message: 'The requested service does not exist.',
          })
        });
      }
    },
  };
  return self;
});

args.forEach((item) => {
  var client = new ThingAccessClient(item.config, item.callbacks);
  client.setup()
    .then(() => {
      return client.registerAndOnline();
    })
    .then(() => {
      // Push events and properties to LinkEdge platform.
      return new Promise(() => {
        setInterval(() => {
          var temperature = item.thing.temperature;
          if (temperature > 40) {
            client.reportEvent('high_temperature', {'temperature': temperature});
          }
          client.reportProperties({'temperature': temperature});
        }, 2000);
      });
    })
    .catch(err => {
      console.log(err);
      return client.cleanup();
    })
    .catch(err => {
      console.log(err);
    });
});

module.exports.handler = function (event, context, callback) {
  console.log(event);
  console.log(context);
  callback(null);
};
```

## Python版本 {#section_rnc_kpx_kfb .section}

```
# -*- coding: utf-8 -*-
import lethingaccesssdk
import time
import json
import os
import logging


# Base on device, user need to implement the callService, getProperties and getProperties function.
class Temperature_device(lethingaccesssdk.ThingCallback):
  def __init__(self):
    self.temperature = 41

  def callService(self, name, input_value):
    return -1, {}

  def getProperties(self, input_value):
    if input_value[0] == "temperature":
      return 0, {input_value[0]: self.LightSwitch}
    else:
      return -1, {}

  def setProperties(self, input_value):
    if "temperature" in input_value:
      self.LightSwitch = input_value["temperature"]
      return 0, {}

device_obj_dict = {}
try:
  driver_conf = json.loads(os.environ.get("FC_DRIVER_CONFIG"))
  if "deviceList" in driver_conf:
    device_list_conf = driver_conf["deviceList"]
    device = device_list_conf[0]
    pk = device["productKey"]
    dn = device["deviceName"]
    app_callback = Temperature_device()
    client = lethingaccesssdk.ThingAccessClient(pk, dn)
    client.registerAndonline(app_callback)
    while True:
      time.sleep(2)
      if app_callback.temperature > 40:
        client.reportEvent('high_temperature', {'temperature': app_callback.temperature})
        client.reportProperties({'temperature': app_callback.temperature})
except Exception as e:
  logging.error(e)

# don't remove this function
def handler(event, context):
  return 'hello world'
```

