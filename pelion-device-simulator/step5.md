The docker image comes already pre-configured with the necessary tools to perform a firmware update. In particular, build tools and the [manifest-tool](https://github.com/PelionIoT/manifest-tool) is included to sign and produce a firmware manifest ready to be uploaded to Pelion portal to start an update campaign. 

> NOTE: For more information about the importantance of manifest and the role it plays in the firmware update process, please consult our [documentation page](https://developer.pelion.com/docs/device-management/current/updating-firmware/firmware-manifests.html).

Let's change the firmware code running on the virtual device, to simulate a code change and subsequent firmware update. Click the ![alt text](https://i.ibb.co/GsHTHLc/katacoda-plus-icon.png "Plus") button to open a new terminal tab. Then:

1. Clone the virtual demo repository locally:

    `git clone https://github.com/PelionIoT/virtual-demo-for-pelion.git && \
    cd virtual-demo-for-pelion`{{execute}}

2. Switch to the directory where the 'firmware' source code is located:

    `cd mbed-cloud-client-example`{{execute}}

3. Copy credential sources and manifest-tool configuration from the running docker container to your local folder:

    `docker cp pelion-demo:/build/mbed-cloud-client-example/mbed_cloud_dev_credentials.c . && \
    docker cp pelion-demo:/build/mbed-cloud-client-example/update_default_resources.c . && \
    docker cp pelion-demo:/build/mbed-cloud-client-example/.manifest-dev-tool .`{{execute}}

4. Using `vi` editor open `main.cpp` and insert the following code to simulate a code change (insert at line :273):

    `vi main.cpp`{{execute}}

    ```
    for (int i=0; i<5; i++) {
    printf("!! new firmware !! \n");
    }
    ```

    Save and exit.

5. Bootstrap a new development container of the virtual demo image to use it for building our new firmware. Notice that we local mount the credential sources and the manifest configuration we copied in step 3 above, so that they are available from inside the new container:

    `docker run -it --name pelion-demo-dev \
    -v $(pwd)/main.cpp:/build/mbed-cloud-client-example/main.cpp \
    -v $(pwd)/mbed_cloud_dev_credentials.c:/build/mbed-cloud-client-example/mbed_cloud_dev_credentials.c \
    -v $(pwd)/update_default_resources.c:/build/mbed-cloud-client-example/update_default_resources.c \
    -v $(pwd)/.manifest-dev-tool/:/build/mbed-cloud-client-example/.manifest-dev-tool/ \
 pelion/virtual-demo bash`{{execute}}

We are now ready to build a new firmware and start an update campaign. Click Continue to move to the next step.