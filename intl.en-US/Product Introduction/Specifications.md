# Specifications

This topic describes the differences between Link IoT Edge Pro, Link IoT Edge Standard, and Link IoT Edge Lite. It also lists the software and hardware requirements for Link IoT Edge editions.

-   You can install Link IoT Edge Pro from Docker-based packages. Link IoT Edge Pro includes all features that are supported by Link IoT Edge.
-   You can install Link IoT Edge Standard from self-contained executable packages. You can select an installation package based on your software or hardware environment.
-   You can install Link IoT Edge Lite from an open-source package. You can use official self-contained packages or build packages from source code. Link IoT Edge Lite supports remote operations and maintenance.

## Features

|Feature|Pro|Standard|Lite|
|:------|:--|:-------|:---|
|Remote SSH service|Supported|Supported|Supported|
|Remote file service|Supported|Supported|Supported|
|Remote web tunnel|Supported|Supported|Supported|
|MQTT migration to the cloud|Supported|Supported|Supported|
|Sub-device management|Supported|Supported|Not supported|
|Driver|Supports C, Node.js, and Python|Supports C and Node.js|Not supported|
|Function Compute business applet|Supports C, Node.js, and Python|Supports C and Node.js|Not supported|
|Visualized scene orchestration|Supported|Supported|Not supported|
|Streaming data analysis|Supported|Not supported|Not supported|
|AI-powered model running framework|Supported|Not supported|Not supported|
|Message routing|Supported|Supported|Not supported|
|Cloud service integration|Supported|Supported|Not supported|
|Application isolation|Container isolation|Process isolation|Not supported|

## Hardware requirements

The following table lists hardware requirements for Link IoT Edge editions.

|Parameter|Pro|Standard|Lite|
|:--------|:--|:-------|:---|
|CPU architecture|x86-64|-   x86-64
-   ARMv8 64-bit
-   ARMv7 VFPv3 hard-float
-   ARMv7 soft-float

|-   x86-64
-   ARMv8 64-bit
-   ARMv7 VFPv3 hard-float
-   ARMv7 soft-float |
|CPU clock speed|Minimum of 2 GHZ|Minimum of 1 GHZ|No limit|
|RAM|Minimum of 2 GB|Minimum of 128 MB|Minimum of 1 MB|
|Disk|Minimum of 2 GB|Minimum of 128 MB|Minimum of 1 MB|

The following table lists software requirements for Link IoT Edge editions.

|Operating system|Pro|Standard|Lite|
|:---------------|:--|:-------|:---|
|Linux|Docker \(later than v17.03\)|-   Kernel version \(2.6.32 or later for x86-64\)
-   Kernel version \(2.6.32 or later for ARMv7 soft-float and hard-float\)
-   Kernel version \(3.7.0 or later for ARMv8 64-bit\)

|-   Kernel version \(2.6.32 or later for x86-64\)
-   Kernel version \(2.6.32 or later for ARMv7 soft-float and hard-float\)
-   Kernel version \(3.7.0 or later for ARMv8 64-bit\) |
|Windows|-   Bash \(such as Git Bash\)
-   Docker \(later than v17.03\)

|Not supported|Not supported|
|macOS|Docker \(later than v17.03\)|Not supported|Not supported|
|Cloud Shell|Not supported|Available only for Link IoT Edge v1.8.2 or later|Not supported|

