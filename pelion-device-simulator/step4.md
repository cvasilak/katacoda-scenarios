Your device is now connected to your Pelion Device Management account. Click on the device ID to view all its information:

![alt text](https://i.ibb.co/Mcn0yCx/portal-device-list.png "Simulator")


The simulator exposes a number of LwM2M resources. LwM2M stands for _"Lightweight Machine to Machine"_ and is the protocol IoT devices use to communicate with the server to receive and execute commands. _"Resources"_ is the name LwM2M gives to the readable and controllable aspects of IoT devices, such as their sensors.

Select the **Resources** tab to view the device's exposed LwM2M resources. Scroll down to locate the **"button_count"**, **"blink_action"** and **"blink_pattern"** resources:

![alt text](https://i.ibb.co/FBLXdxy/portal-resources.png "Simulator")

The simulator exposes the **"button_count"** resource to track the number of button presses occuring in the device. It actually simulates the button presses by periodically emitting the press event every 5 secs, thus the _"Simulated.."_ log messages you see in the simulator console:

![alt text](https://i.ibb.co/d4bKHHK/portal-console-simulated.png "Console")

Click on the **"button_count"** resource to open the graph and see the current button press count. Notice that the graph updates itself periodically as the value of the resource changes on the device:

![alt text](https://i.ibb.co/XZr5D07/portal-button-count-graph.png "Button Count")


The **"blink_action"** 


**"blink_pattern"**