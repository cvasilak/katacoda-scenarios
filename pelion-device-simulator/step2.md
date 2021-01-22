Let's assign the **Access Key** retrieved from the previous step to a shell variable for easy reference. Copy the key to your clipboard and then click on the command below to fill it in the terminal. Then paste the key and press <kbd>Enter<kbd>

`export ACCESS_KEY=`{{execute no-newline}}

We are now ready to launch the virtual demo. Click on the command below to launch the Docker container that bootstraps the demo:

`docker run -it --name pelion-demo --net host -e CLOUD_SDK_API_KEY=$ACCESS_KEY pelion/virtual-demo`{{execute}}

It takes some time for the command to finish since it needs to download the virtual-demo image, retrieve the developer certificate from Pelion portal and then proceed to build the application. Once it finishes, it would print out the following in the console, marking a successfully connection to Pelion Device Management service:

![alt text](https://i.ibb.co/fYbR7ff/portal-demo-ready.png "Ready")

We are now ready to visit the virtual-demo page. Click Continue to move to the next step.
