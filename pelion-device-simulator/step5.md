The docker image comes already pre-configured with the necessary tools to perform a delta firmware update. In particular, build tools and the suite of tools from [manifest-tool](https://github.com/PelionIoT/manifest-tool) are included to a) create a delta firmware image and b) sign and produce a firmware manifest ready to be uploaded to Pelion portal to start an update campaign. 

> NOTE: For more information about the importance of manifest and the role it plays in the firmware update process, please consult our [documentation page](https://developer.pelion.com/docs/device-management/current/updating-firmware/firmware-manifests.html).

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

4. Since we are planning to create a delta image, we need to save the existing running firmware to be able to produce a delta:

    `mkdir firmwares && \
    docker cp pelion-demo:/build/mbed-cloud-client-example/__x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf ./firmwares/current_fw.bin`{{execute}}

5. Let's alter the emitted simulated vibration value sent by the virtual demo to be multipled by 1000. Using `vi` editor, open `source/blinky.cpp` and change the line to the following (line :295):

    `vi source/blinky.cpp`{{execute}}

    ```
    _sensed_count = randomvib * 1000;
    ```

    Save and exit.

6. Bootstrap a new development container of the virtual demo image to use it for building our new firmware. Notice that we local mount the credential sources, the manifest configuration and the running firmware folder we copied in step 3 above, so that they are available from inside the new container:

    `docker run -it --name pelion-demo-dev \
    -v $(pwd)/source/blinky.cpp:/build/mbed-cloud-client-example/source/blinky.cpp \
    -v $(pwd)/mbed_cloud_dev_credentials.c:/build/mbed-cloud-client-example/mbed_cloud_dev_credentials.c \
    -v $(pwd)/update_default_resources.c:/build/mbed-cloud-client-example/update_default_resources.c \
    -v $(pwd)/.manifest-dev-tool/:/build/mbed-cloud-client-example/.manifest-dev-tool/ \
    -v $(pwd)/firmwares/:/build/mbed-cloud-client-example/firmwares \
 pelion/virtual-demo bash`{{execute}}

We are now ready to build a new firmware and start an update campaign. Click Continue to move to the next step.