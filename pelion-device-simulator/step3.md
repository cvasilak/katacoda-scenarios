Visit the simulator page by clicking the `Simulator` tab at the top of the screen:

![alt text](https://i.ibb.co/XtvtMPc/portal-simulator-tab.png "Simulator")

> NOTE: If you are presented with an _"Unable to connect"_ error message upon clicking on the tab, don't worry! Because the simulator takes some time to start, the platform timeouts attempting to connect. Click either the "Try Again" or hit the Refresh button ![alt text](https://i.ibb.co/YtMtg4x/refresh.png "Refresh") to manually connect.

You should be presented with the following screen:

![alt text](https://i.ibb.co/MkHfbbm/portal-simulator-connected.png "Connected")

Notice the simulator printing out the **"Endpoint Name"** after the successfully connection to Pelion Device Management Service.

If you now [visit the Device List](https://portal.mbedcloud.com/devices/list) in Pelion portal, it should display the device as <span style="color:green">'_Registered_'</span>

![alt text](https://i.ibb.co/5KCYDSv/pelion-portal-connected.png "Connected")

Let's add a simulated LED component and connect it to the board. Click the `Add Component` button at the top of the screen:

![alt text](https://i.ibb.co/vhN25q6/simulator-add-component.png "Add component")

From the dialog that appears, select `Red LED` from the list and use `LED1` as the board pin: 

![alt text](https://i.ibb.co/g3SVmTG/simulator-add-component-dialog.png "Add component")

An LED component should now appear on the right of the board:

![alt text](https://i.ibb.co/bKmBrpg/simulator-led.png "Led")

We are now ready to interact with the device through the Pelion portal. Click Continue to move to the next step.