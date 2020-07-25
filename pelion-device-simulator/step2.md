Let's assign the **API_Key** retrieved from the previous step to a shell variable for easy reference. Copy the key to your clipboard and then click on the command below to fill it in the terminal. Once down, paste the key and press <kbd>Enter<kbd>

`export API_KEY=`{{execute no-newline}}

We are now ready to launch the simulator. Click on the command below to launch the Docker container that  bootstraps the simulator:

`docker run -it --net host -e CLOUD_SDK_API_KEY=$API_KEY pelion/device-simulator`{{execute}}

It takes some time for the command to finish since it needs to download the simulator image, retrieve the developer certificate from Pelion portal and then proceed to build the application. Once it finishes, it would print out the following in the console:

![alt text](https://i.ibb.co/WNXpRzF/portal-sim-ready.png "Ready")

We are now ready to visit the simulator page. Click Continue to move to the next step.
