---
keyword: [scene orchestration in the cloud, create a scene rule]
---

# Scene orchestrations in the cloud

The rules for scene orchestration allow you to automate workflows based on the specified business logic in a visualized way. You can configure time or device-based triggers and conditions for rules. These rules can execute actions that change the statuses of other rules, devices, or functions. This allows you to implement scene orchestration for a large number of devices.

An edge instance is created. For more information, see [Set up environments](/intl.en-US/Link IoT Edge/User Guide/Set up environments/Link IoT Edge Pro Edition/Install Link IoT Edge on Ubuntu 16.04.md).

## Create scene rules

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com).

2.  In the left-side navigation pane, choose **Rules** \> **Scene Orchestration**.

3.  Click **Create Rule**.

    ![Scene Orchestration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3926009851/p6572.png)

4.  Set the parameters as required and click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |Rule Name|The name of the rule. The rule name must be 1 to 30 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\).|
    |Rule Description|Optional. The description of the rule.|

5.  After the scene rule is created, click **Edit** in the message that appears to configure the rule.

    You can also configure the scene rule by clicking **View** next to the rule name.

    For example, you can use a scene rule to automate an air conditioner. When the indoor temperature that is reported by the temperature sensor between 12:00 and 23:59 is lower than 16°C, the air conditioner automatically raises the indoor temperature to 26°C.

    The following figure shows the parameter configurations.

    ![Set up scene orchestration parameters](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3926009851/p6573.png)

    In the upper-right corner of the page, click **Edit** to change the name of the scene rule. For more information about other parameters, see the following table.

    |Parameter|Description|
    |---------|-----------|
    |Trigger|The triggers that set off the rule. You can set this parameter to **Device Trigger** or **Timed Trigger**. When the reported device data or the current time meets the triggers, the system checks whether the conditions to trigger the rule are met. You can create one or more triggers for a rule. The rules are related by logic OR operations.     -   If you set this parameter to **Device Trigger**, you must select an existing product, one or all devices, and one or all properties or one or all events.
    -   If you set this parameter to **Timed Trigger**, you must specify a point in time. The time must be specified by using a CRON expression. A CRON expression consists of the following five fields: the minute, hour, day, month, and day of a week. For the day of a week, a value of 0 or 7 indicates Sunday and values of 1 to 6 indicate Monday to Saturday. Separate these fields with spaces. For example, you can write a CRON expression to trigger a rule every day at 18:00 in the `0 18 * * *` format. You can also write a CRON expression to trigger a rule every Friday at 18:00 in the `0 18 * * 5` format. The asterisks \(\*\) are wildcards. For more information about how to write a CRON expression, see [CRONTAB](http://crontab.org/).

In the preceding example, this parameter is set to **Device Trigger**. In this case, the trigger refers to a scenario where the indoor temperature reported by the temperature sensor is lower than 16°C. |
    |Condition|The set of conditions. The rule is triggered only when the data meets all conditions. You can set this parameter to **Device Status** or **Time Range**. You can create one or more conditions for a rule. The conditions are related by logical AND operations.     -   If you set this parameter to **Device Status**, you must select an existing product, a device of the product, and a property or event of the device feature.
    -   If you set this parameter to **Time Range**, you must specify the start time and end time in the `yyyy-mm-dd hh24:mi:ss` format.
In the preceding example, this parameter is set to **Time Range** and the rule can be triggered between 12:00 and 23:59. |
    |Action|The action to be performed. You can create one or more actions. When an action fails, it does not affect other actions.     -   If you set this parameter to **Device Output**, you must select an existing product, a device of the product, and a property or service of the device feature. Only writable properties or services can be selected to perform the action. IoT Platform performs the actions based on the defined device properties or services when both the triggers and the conditions for the rule are met.
    -   If you set this parameter to **Rule Output**, you must select another rule and the action will invoke the selected rule. The triggers for the invoked rule are skipped and only the conditions of the rule are checked. If the conditions are met, the actions that are defined in the invoked rule is performed.

For example, if Rule A is triggered, the triggers of Rule A are skipped. The conditions of Rule A are checked. If all conditions of Rule A are met, IoT Platform performs the actions of Rule A. The conditions are related by logical AND operations.

In the preceding example, this parameter is set to **Device Output**. In this case, when the rule is triggered, the air conditioner will raise the temperature to 26°C. |
    |Delayed Execution|This parameter is displayed after you show the advanced options. After you set this parameter, the specified actions are executed after a specified period of time. Valid values: 0 to 86400. Unit: seconds.|


## Start scene rules

After a scene rule is created, you can start the scene rule on the Scene Orchestration page.

You can perform the following steps to start a scene rule:

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com). In the left-side navigation pane, choose **Rules** \> **Scene Orchestration**.

2.  Find the scene rule that you want to start and click **Start**. The rule status changes to **Running**.

    ![Start a scene rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3926009851/p6574.png)


After you start the rule:

-   If the scene rule runs on the cloud, you must configure message routing for the devices of the scene rule. This allows the device properties and events to be sent to IoT Hub that runs on the cloud. For more information about how to configure a message route, see [Configure message routing](/intl.en-US/Link IoT Edge/User Guide/Message routing/Configure message routing.md).
-   If the scene rule runs at the edge, you must stop running the scene rule in the cloud and associate the scene rule with the edge instance. For more information, see [Other operations for scene orchestration](#section_lv6_7wr_zox).

## View logs

You can view the logs of scene rules and view the results on the details page.

**Note:** A scene rule can run on the cloud and at the edge at the same time. In this case, to view all the logs of the scene rule, perform the following steps: Log on to the IoT Platform console and choose **Rules** \> **Scene Orchestration**.

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com). In the left-side navigation pane, choose **Rules** \> **Scene Orchestration**.

2.  Find the scene rule that you want to view and click **Log** on the right.

3.  Click **Details** to view the log details.

    ![View scene orchestration logs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4926009851/p6575.png)

    **Note:** If the status of a log is Failed, you can click **Details** in the Actions column to view the details of execution failures.


## Other operations for scene orchestration

-   Delete scene rules:
    1.  On the Scene Orchestration page, find the rule that you want to delete.
    2.  Click **Delete** next to the rule name. In the message that appears, click **OK** to delete the scene rule.
-   Trigger scene rules:

    You can trigger a scene rule after you start the rule.

    1.  On the Scene Orchestration page, find the rule that you want to trigger.
    2.  Click **Trigger** next to the rule name, and the rule is manually triggered once. All actions of the rule are performed regardless of the specified triggers.
-   Run a scene rule on an edge instance:

    Perform the following steps to deploy a scene rule on the edge instance.

    **Note:** Make sure that you have stopped running the scene rule in the cloud.

    1.  Log on to the [Link IoT Edge console](https://iot.console.aliyun.com/le/instance/list). In the left-side navigation pane, click **Edge Instances**. Find the edge instance that you created and click **View** in the Actions column.
    2.  On the Instance Details page, click the **Scenes** tab. Then, click **Assign Scene**.
    3.  In **Assign Scene** panel, click **Assign** next to the rule name. Then, click **Close**.

        ![Assign the scene rule to an edge instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4926009851/p39451.png)

    4.  After the scene rule is assigned, redeploy the edge instance.

