Your device is now connected to your Pelion Device Management account. Click on the device ID to reveal more information:

![alt text](https://i.ibb.co/NtzBDqW/portal-device-details.png "Pelion Virtual Demo")

The tool exposes a number of LwM2M resources. LwM2M stands for [_"Lightweight Machine to Machine"_](https://omaspecworks.org/what-is-oma-specworks/iot/lightweight-m2m-lwm2m/) and is an open, efficient, vendor-neutral and standardized device management protocol ([spec](http://www.openmobilealliance.org/release/LightweightM2M/V1_0_2-20180209-A/OMA-TS-LightweightM2M-V1_0_2-20180209-A.pdf)) IoT devices use to communicate with the server to send telemetry data and to invoke actuator commands. _"Resources"_ is the name LwM2M gives to the readable and controllable aspects of IoT devices, such as their sensors.

Select the **Resources** tab in the Device details pane to view the device's exposed LwM2M resources. Scroll down to locate the **"blink_resource"**, **"pattern_resource"** and **"vibration_resource"** resources:

![alt text](https://i.ibb.co/ZHJjpkr/portal-resources.png "Pelion Virtual Demo")

## Subscribing to Resource changes

The **"vibration_resource"** tracks the Vibration sensor readings emitted by the device. The value displayed in the LCD screen and the LwM2M resource should stay in-sync going forward. If you switch to the Terminal tab, the following log messages are periodically printed by the device to verify the successfully delivery of the sensor reading to Pelion service:

![alt text](https://i.ibb.co/1Z9Qk7H/portal-console-simulated.png "Console")

Click on the **"vibration_resource"** to view a graphical representation of the current value. Notice that the graph updates itself periodically as the value of the resource changes on the device:

> NOTE: To minimize the network traffic, the device does not start sending notifications of Resource changes automatically. Instead, the Pelion portal _subscribed_ to the **"vibration_resource"** on the device to _observe_ the changes, thus the _"Subscribed"_ log message you see in the console:
> 
>![alt text](https://i.ibb.co/6WrRGqR/portal-subscribed-log.png "Subscribe log")

![alt text](https://i.ibb.co/P9MrFr1/portal-vibration-graph.png "Button Count")

Now, click the ![alt text](https://i.ibb.co/m0fd8RT/shake-btn.png "Shake") button to put the demo device into a high vibration mode and you can see the larger vibration readings coming through to Pelion!

## The Execute operation

Close the dialog box and then click on **"blink_resource"** resource to execute an operation on the device. In particular, when invoked the LED component on the device will start blinking. On the dialog box that appears, click the edit ![alt text](https://i.ibb.co/Yhr1vDH/portal-edit.png "Edit") button, select the ![alt text](https://i.ibb.co/YchBzn5/portal-post.png "Post") tab and click ![alt text](https://i.ibb.co/42LHD2s/portal-send.png "Send")

![alt text](https://i.ibb.co/mXS0xGH/portal-execute-operation.png "Execute")

When the device receives the message, the LED component will start blinking!

![alt text](https://i.ibb.co/xMbvB0y/blinking-action.gif "Execute log")

and in the log console the received _"actuator"_ message from the portal is logged:

![alt text](https://i.ibb.co/93qc886/pelion-execute-log.png "Execute log")

## The Read / Write operation

The device blinks the LED based on a pattern stored in its **"pattern_resource"**. Initially, it is set to `"500:500:500:500:500:500:500:500"`, where each number represents the number of milliseconds the LED will stay on. Let's update this resource and lower the millisecond delay to make the blinking go faster!

Click on the **"pattern_resource"** resource to open the dialog that displays the current value. Click the edit ![alt text](https://i.ibb.co/Yhr1vDH/portal-edit.png "Edit") button, select the ![alt text](https://i.ibb.co/5rVrVv4/portal-put.png "Put") tab and change the value to `
100:100:100:100:100:100:100:100`. Once done, click ![alt text](https://i.ibb.co/42LHD2s/portal-send.png "Send"):

![alt text](https://i.ibb.co/VxPGGGy/portal-write-resource.png "Write")

Once the device receive the message, it logs it in the console and updates the value of the **"pattern_resource"** with the new value:

![alt text](https://i.ibb.co/JzNk522/portal-write-log.png "Write log")

If you now try to invoke again the **"blink_resource"** from the previous step, the blinking of the LED should go faster!

Now that we have demonstrated basic interactions with the device, let's update the running firmware to a new version. Click Continue to move to the next step.