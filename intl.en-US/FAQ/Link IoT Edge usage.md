# Link IoT Edge usage

This topic lists common questions about Link IoT Edge usage and provides answers to them.

## If I want to use the resumable download feature, do I need to make extra development in addition to specifying QoS when configuring a message route?

No, extra development is not required. For more information about the resumable download feature, see [Resume data transmission from a breakpoint](/intl.en-US/User Guide/Resume data transmission from a breakpoint.md).

## How do I enable an ECS instance to receive data that a sub-device reports to IoT Platform through the gateway?

Use the data forwarding feature provided by Rules Engine in IoT Platform to forward device data to a specific topic you defined. Configure your ECS instance to call the specific API operation of IoT Platform to subscribe to the topic and obtain required data. For more information, see [Data Forwarding](/intl.en-US/Communications/Data Forwarding/Overview.md).

