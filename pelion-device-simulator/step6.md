Now that our environment is set up, we are ready to build the new firmware and prepare for an update campaign:

1. Switch to the firmware source code directory:

    `cd /build/mbed-cloud-client-example/`{{execute}}

2. Build the new firmware image by invoking the `make` tool:

    `make -C __x86_x64_NativeLinux_mbedtls/ mbedCloudClientExample.elf`{{execute}}

3. Upon completion of the build, a new firmware binary is generated:

    ```
    $ ls -l /build/mbed-cloud-client-example/__x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf

    -rwxr-xr-x 1 root root 6564528 Jan 27 10:42 mbedCloudClientExample.elf
    ```

4. Copy the new firmware to `firmwares/` directory:

    `cp __x86_x64_NativeLinux_mbedtls/Debug/mbedCloudClientExample.elf firmwares/new_fw.bin`{{execute}}

5. The `firmwares/` directory should now contain both the new firmware(`new_fw.bin`) and the currently running one(`current_fw.bin`):

    ```
    ls -l firmwares/

    total 13M
    -rwxr-xr-x 1 root root 6564528 Jan 27 10:30 current_fw.bin
    -rwxr-xr-x 1 root root 6564528 Jan 27 10:43 new_fw.bin
    ```

6. We are now ready to generate a delta firmware using the `manifest-delta-tool`:

    `manifest-delta-tool -c firmwares/current_fw.bin -n firmwares/new_fw.bin -o firmwares/delta-patch.bin`{{execute}}

    We should get the following output upon successfully completion:

    ```
    2021-01-27 10:44:30,382 INFO Current tool version PELION/BSDIFF001
    Wrote diff file firmwares/delta-patch.bin, size 325726. Max undeCompressBuffer frame size was 512, max deCompressBuffer frame size was 202.
    ```

    If we list the directory contents, we can verify the producing of the `delta-patch.bin` firmware. Notice the significant shrinkage in size, from 6.3MB of a full firmware image, down to a delta of 240K!

    ```
    ls -l firmwares/delta-patch.bin

    -rw-r--r-- 1 root root  325726 Jan 27 10:44 delta-patch.bin
    ```

Now that our new firmware is produced, we are ready to start an update campaign. Click Continue to move to the next step.