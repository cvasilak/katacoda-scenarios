Now that our environment is setup, we are ready to build the new firmware and start an update campaign:

1. Switch to the firmware source code directory:

    `cd /build/mbed-cloud-client-example/`{{execute}}

2. Build the new firmware image by invoking the `make` tool:

    `make -C __x86_x64_NativeLinux_mbedtls/ mbedCloudClientExample.elf`{{execute}}

3. Upon completion of the build, a new firmware binary is generated:

    ```
    $ ls -l /build/mbed-cloud-client-example/__x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf

    -rwxr-xr-x 1 root root 6562112 Jan 19 14:32 /build/mbed-cloud-client-example/__x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf
    ```

4. We now need to genarate the firmware manifest describing the update, upload it to the portal and start the update campaign. The `manifest-tool` can conveniently perform all this in one step. Simple execute:

    `manifest-dev-tool update -p __x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf -w -n -v 0.2.0`{{execute}}
    
    Upon executing the command, notice the firmware binary being uploaded to Pelion, the generation of the manifest and the starting of the update campaign: 

    ```
    INFO FW version: 0.2.0
    INFO Uploading FW image __x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf
    INFO Uploaded FW image http://firmware-catalog-media-ca57.s3.
    INFO Vendor-ID: f214c5a40a7c41588f4a8f2357880e4a
    INFO Class-ID: 66eb99760e98456d8436dc223c7332ff
    INFO Created manifest in v3 schema for full update campaign
    INFO Uploaded manifest ID: 01771ad664fd0000000000010010028e
    INFO Created Campaign ID: 01771ad6669b00000000000100100323
    INFO Started Campaign ID: 01771ad6669b00000000000100100323
    INFO Campaign state: publishing
    INFO Campaign state: autostopped
    INFO Campaign is finished in state: autostopped
    INFO ----------------------------
    INFO     Campaign Summary
    INFO ----------------------------
    INFO  Successfully updated:   1
    INFO  Failed to update:       0
    INFO  Skipped:                0
    INFO  Pending:                0
    INFO  Total in this campaign: 1
    ```

    If you switch to the first terminal, notice that the device logs the downloading of the new firmware, the verification of the manifest and the successfull update: 

    ```
    [FOTA INFO] fota.c:596: Firmware update initiated.
    [FOTA DEBUG] fota.c:628: Pelion FOTA manifest is valid
    [FOTA DEBUG] fota.c:651: get manifest : curr version 131072, new version 196608
    ...
    ...
    [FOTA DEBUG] fota.c:555: Download Authorization requested
    [FOTA] ---------------------------------------------------
    [FOTA] Updating component MAIN from version 0.0.0 to 0.2.0
    [FOTA] Update priority 0
    [FOTA] Update size 6562112B
    [FOTA] ---------------------------------------------------
    [FOTA] Download authorization granted
    ...
    [FOTA] Downloading firmware. 0%
    [FOTA] Downloading firmware. 5%
    [FOTA] Downloading firmware. 10%
    [FOTA] Downloading firmware. 15%
    ...
    [FOTA INFO] fota.c:804: Installing new version for component MAIN
    [FOTA INFO] fota_candidate.c:224: Found an encrypted image at address 0x0
    [FOTA INFO] fota_candidate.c:416: Validating image...
    [FOTA INFO] fota_candidate.c:461: Image is valid.
    [FOTA INFO] fota_component.c:189: Installing MAIN component
    [FOTA] Successfully installed MAIN component
    ...
    [FOTA INFO] fota.c:725: Rebooting.
    !! new firmware !!
    !! new firmware !!
    !! new firmware !!
    !! new firmware !!
    !! new firmware !!
    In single-partition mode.
    Creating path ./pal
    Start Device Management Client
    ```

    This is also reflected in Pelion update campaign dashboard, showing the successfull completion of the update:

    ![alt text](https://i.ibb.co/bPyvFw8/portal-campaign-dashboard.png "Plus")

    and the device displays the new firmware version (0.2.0 in our case):

    ![alt text](https://i.ibb.co/dp1fMYf/device-fw-version.png "Plus")
