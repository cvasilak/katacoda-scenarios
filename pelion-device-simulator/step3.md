Visit the demo page by clicking the `Virtual Demo` tab at the top of the screen:

![alt text](https://i.ibb.co/svJ6zP2/portal-simulator-tab.png "Simulator")

> NOTE: If you are presented with an _"Unable to connect"_ error message upon clicking on the tab, don't worry! Because the container image takes some time to start, the platform timeouts attempting to connect. Click either the "Try Again" link or hit the Refresh button ![alt text](https://i.ibb.co/YtMtg4x/refresh.png "Refresh") to manually connect.

You should be presented with the following screen:

![alt text](https://i.ibb.co/TW14x5d/portal-simulator-connected.png "Connected")

The LCD screen at the top, displays the current "simulated" vibration reading which is automatically updated with a new value every five seconds. The Device ID as obtained from Pelion and the current running Firmware version are also displayed.

At the bottom, you can see three tick boxes reflecting the provisioning state of the device and the encryption of all messaging between the device and the Pelion service. This virtual demo uses a development certificate obtained from Pelion when the demo first bootstrapped (using your `ACCESS_KEY`) and utilize it to make the connection to the service. When the first connection is made, the device presents the certificate to the service to be validated, the service then validates back and a mutual trust is established. All messaging is encrypted, so its not possible to inject false certificates or monitor the connection - we prevent other, unauthorised devices from pushing untrusted data into your IoT system.

If you now [visit the Device List](https://portal.mbedcloud.com/devices/list) in Pelion portal, it should display the device as <span style="color:green">'_Registered_'</span>

![alt text](https://i.ibb.co/S6c5Hh2/pelion-portal-connected.png "Connected")

We are now ready to interact with the device through the Pelion portal. Click Continue to move to the next step.