## Launch Simulator
Let's assign the _API_Key_ retrieved from the previous step to a shell variable for easy reference:

`export API_KEY=`{{execute no-newline}}

We are now ready to launch the simulator:

`docker run -it --net host -e CLOUD_SDK_API_KEY=$API_KEY pelion/device-simulator`{{execute}}

### Access it
[https://[[HOST_SUBDOMAIN]]-7829-[[KATACODA_HOST]].[[KATACODA_DOMAIN]]]
