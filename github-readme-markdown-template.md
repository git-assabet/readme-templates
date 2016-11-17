# Title or Project Name
date or release: 2016/06/20

[comment]: <> (This is a comment, it will not be included in the output as long as there is a blank line above the comment block)

<!---
your comment goes here
and here
-->

The demo project source is available on github: https://github.com/demo-path. Contact Xively with your github username for access to the repo.

## Development tools

[comment]: <> (list the components used to build the project)

The demo was built using the following components:
* CC3200 SDK: V 1.1.0
* CC32xx Service Pack: V 1.1.0
* Code Composer Studio: V 6.1.0.00104

Installed at:
* C:\ti\CC3200SDK_1.1.0
* C:\ti\CC31xx_CC32xx_ServicePack_1.0.0.10.0
* C:\ti\ccsv6

The demo is based on the following SDK examples:
* freertos_demo
* tftp_client

## Prerequisites

[comment]: <> (list all tools, configurations, licenses, etc needed for this project)
- TI Code Composer Studio
- TI CC3200 SDK
- The WIFI Credentials for each device must be configured for a local WIFI network.
See the section: Flash update, WIFI Credentials
- In the `.\xively_demo\main.h` file, set the following parameters:
    ```
    #define SSID
    #define SSID_KEY
    #define SEC_TYPE
    ```
- Optional: In the `.\xively_demo\main.h` file, adjust the value of the following parameter to your needs:
    ```
    #define XM_BUILD_DEVICE 1 
    ```

## Installation / Building 

TI Code Composer Studio should be stated with the git repo directory,
`...\uponor-demo`, as the workspace directory, the `xively_demo` project should
then be imported and built.

After a successful build, a binary image file is
created:
  `...\uponor-demo\xively_demo\Debug\xively_demo.bin`
and copied to:
  `...\uponor-demo\UniFlash\xively_demo.bin`

### Updating flash
Required tools: TI UniFlash

1. Configure WIFI credentials:
    1. Update `...\uponor-demo\UniFlash\wifi.cfg` with local WIFI credentials.
    2. Run UniFlash application.
    3. Open configuration `...\uponor-demo\UniFlash\config_wifi\config_wifi.usf`.
    4. Program the device.
2. Load firmware image:
    1. Build firmware.
    2. Run UniFlash application.
    3. Open configuration `...\UniFlash\load_firmware\load_firmware.usf`.
    4. Program the device.
3. Update Xively credentials:
    1. Update `...\uponor-demo\UniFlash\xively_deviceX.cfg` with credentials from Xively CPM.
    2. Run UniFlash application.
    3. Open configuration `uponor-demo\UniFlash\config_deviceX\config_deviceX.usf`.
    4. Program the device.

### CC3200 LaunchPad configuration

The default hardware configuration of the CC3200 LaunchPad has been modified to
support simultaneous use of all features; the I2C configuration was modified.

|   | Default | Modified |
|---|----|---|
| Interface |  I2C0  |  I2C0 | 
| SCL | PIN01, CC_GPIO_10, J3 | PIN05, CC_GPIO_14, Red |   
| SDA | PIN02, CC_GPIO_11, J2 | PIN06, CC_GPIO_15, Yellow | 

## Xively CPM operation 

Xively CPM provides basic monitoring and control of the demo devices. 
1. Go to: https://app.xively.com/login.
2. Use the following CPM Credentials:
    * account_id: aaaa1111-33c0-de23-82b4-1111aaaa11aa 
    * email: app1111aaaa@xively.com 
    * password: 1111aaaa1111aaaa1111aaaa1111aaaa1111+a/JxZY=
3. In the left hand frame, select: "All devices".
4. In the center frame, select; "CC3200-Demo-DeviceX".
5. In the center frame, select the "Messaging" tab.

Messages published by the device are displayed in "SHOWING", the following channels are supported: \
`
SW_02
SW_03
LED_GRN_VAL 
LED_YEL_VAL 
LED_RED_VAL 
ACCEL 
TEMPERATURE
`

Messages can be sent to the device using "PUBLISH TO", the following channels are supported: \
`
LED_GRN_SET 
LED_YEL_SET 
LED_RED_SET
`

## Device operation

### Buttons
Channels: `SW_02 SW_03`

Each button publishes a message to Xively when pressed. An example value is: `,/SW_02,1,pushed`

### LED
Channels: `LED_GRN_SET LED_YEL_SET LED_RED_SET`

The state of each LED is controlled with via messages received from Xively. Values are: "ON" or OFF"

Channels: `LED_GRN_VAL LED_YEL_VAL LED_RED_VAL`

A message is published to Xively when a LED state changes. Values are: "ON" or OFF"

### Accelerometer
Channel: `ACCEL`

A message is published to Xively when the orientation of the accelerometer changes. An example value is: `{"X": 0.0469, "Y": 0.0469, "Z": 1.0000}`

### Temperature Sensor
Channel: `TEMPERATURE`

A message is published to Xively when a temperature change is detected. An example value is: `{"celsius": 26.63}`


### Device console

The CC3200 LaunchPad provides a USB Serial Port interface which is
used by the device as an output console.

Serial port settings:
```
    115200
    8 bits
    No parity
    1 stop bit
    No flow control
```

[comment]: <> (This is a comment, it will not be included in the output as long as there is a blank line above the comment block)

### Notes

2015/12/22(R1) : Added support to LibXively to use SimpleLink's secure socket implementation, rather than Xively's SSL library.  Support is only provided for a single Root CA certificate with a fixed filename "/cert/halo_temp_cert.der".

2015/11/20(R1) : Added "xtest_malloc.c" to analyze heap usage. \
Bug Fix: Publish messages in-flight count must be cleared prior to connect/reconnect.

2015/11/19(R1) : This release is functionally equivalent to that of 2015/10/19; but with support for release via Github.
