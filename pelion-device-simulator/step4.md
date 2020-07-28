Your device is now connected to your Pelion Device Management account. Click on the device ID to view all its information:

![alt text](https://i.ibb.co/Mcn0yCx/portal-device-list.png "Simulator")

The simulator exposes a number of LwM2M resources. LwM2M stands for _"Lightweight Machine to Machine"_ and is the protocol IoT devices use to communicate with the server to receive and execute commands. _"Resources"_ is the name LwM2M gives to the readable and controllable aspects of IoT devices, such as their sensors.

Select the **Resources** tab to view the device's exposed LwM2M resources. Scroll down to locate the **"button_count"**, **"blink_action"** and **"blink_pattern"** resources:

![alt text](https://i.ibb.co/FBLXdxy/portal-resources.png "Simulator")

## Subscribing to Resource changes

The **"button_count"** resource tracks the number of button presses occuring in the device. It actually simulates the button presses by periodically emitting the _'press event'_ every 5 secs, thus the _"Simulated.."_ log messages you see in the console:

![alt text](https://i.ibb.co/d4bKHHK/portal-console-simulated.png "Console")

Click on the **"button_count"** resource to open the graph and see the current button press count. Notice that the graph updates itself periodically as the value of the resource changes on the device:

> NOTE: To minimize the network traffic, the device does not start sending notifications of Resource changes automatically. Instead, the Pelion portal _subscribed_ to the **"button_count"** resource on the device to _observe_ the changes, thus the _"Subscribed/Sent/Delivered"_ log messages you see in the console:
> 
>![alt text](https://i.ibb.co/9pssQNK/portal-subscribed-log.png "Subscribe log")

![alt text](https://i.ibb.co/XZr5D07/portal-button-count-graph.png "Button Count")

## The Execute operation

Close the dialog box and then click on **"blink_action"** resource to execute an operation on the device. In particular, when invoked the LED component on the device will start blinking. On the dialog box that appears, click the edit ![alt text](https://i.ibb.co/Yhxffdb/portal-edit.png "Edit") button, select the ![alt text](https://i.ibb.co/GQnYHry/portal-post.png "Post") tab and click ![alt text](https://i.ibb.co/h8QRChy/portal-send.png "Send")

![alt text](https://i.ibb.co/mXS0xGH/portal-execute-operation.png "Execute")

The LED component we added in the previous step will start blinking, and in the log console the received _"actuator"_ message from the portal is logged:

![alt text](https://i.ibb.co/d6w6hQm/pelion-execute-log.png "Execute log")

## The Read / Write operation

If you notice the log from the previous step, the simulator blinks the LED based on a pattern stored in its **"blink_pattern"** resource. Initially, it is set to `"500:500:500:500:500:500:500:500"`, where each number represents the number of milliseconds the LED will stay on. Let's update this resource and lower the millisecond delay to make the blinking go faster.

Click on the **"blink_pattern"** resource to open the dialog that displays the current value. Click the edit ![alt text](https://i.ibb.co/Yhxffdb/portal-edit.png "Edit") button, select the ![alt text](https://i.ibb.co/qgZh1Mx/portal-put.png "Put") tab and change the value to `
100:100:100:100:100:100:100:100`. Once done, click ![alt text](https://i.ibb.co/h8QRChy/portal-send.png "Send"):

![alt text](https://i.ibb.co/VxPGGGy/portal-write-resource.png "Write")

Once the device receive the message, it logs it in the console and updates the value of the **"blink_pattern"** resource with the new value:

![alt text](https://i.ibb.co/nr4sLzw/portal-write-log.png "Write log")

If you now try to invoke again the **"blink_action"** resource from the previous step, the blinking of the LED should go faster!
