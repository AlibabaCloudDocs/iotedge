---
keyword: [edge scene orchestration, scene orchestration]
---

# What is scene orchestration?

Scene orchestration is a feature that is provided by the rules engine of IoT Platform. Scene orchestration provides a way of automating complex workflows based on business logic. You can use scene orchestration rules to set up complex interactions between devices and deploy the rules in the cloud or at the edge.

To create a scene orchestration rule, perform the following steps: Log on to the [IoT Platform console](https://iot.console.aliyun.com/) and choose **Rules** \> **Scene Orchestration**. On the page that appears, create a scene orchestration rule. Each scene orchestration rule consists of triggers, conditions, and actions. This rule model is called the TCA model. TCA is short for triggers, conditions, and actions.

**Note:** Only public instances in the China \(Shanghai\) region support the scene orchestration feature.

When an event or property change that is defined in a trigger occurs, IoT Platform checks whether to perform the actions that are defined in the rule based on the defined conditions. If the conditions are met, IoT Platform performs the defined actions. Otherwise, IoT Platform does not perform the actions.

Assume that you come home from work at 18:00 every day. In the summer, you hope that the indoor temperature is cool and comfortable when you get home. In this case, you can create a rule to automate the air conditioner.

The following figure shows the parameter settings.

![Edit a scene orchestration rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0316009851/p6486.png)

The following table describes the parameters.

|Parameter|Description|Logical operator|
|---------|-----------|----------------|
|Trigger|This rule is triggered at 18:00 every day. For more information about how to write a CRON expression, see [CRONTAB](http://crontab.org/).|Or \(\|\|\)|
|Condition|If the indoor temperature that is reported by a temperature sensor is higher than 26°C, the action is performed.|And \(&&\)|
|Action|Switches the air conditioner on. The temperature for the air conditioner is set to 26°C.|And \(&&\)|

For more information about how to create scene orchestration rules, see [Scene orchestration on the cloud](/intl.en-US/Link IoT Edge/User Guide/Scene orchestration/Scene orchestrations in the cloud.md).

