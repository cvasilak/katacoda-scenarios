We now need to genarate the firmware manifest describing the update, upload it to the portal and start the update campaign. The `manifest-tool` can conveniently perform all this in one step. Simple execute:

`manifest-dev-tool update -p firmwares/delta-patch.bin -w -n -v 0.2.0`{{execute}}
    
Upon executing the command, notice the firmware binary being uploaded to Pelion, the generation of the manifest and the starting of the update campaign: 

```
INFO FW version: 0.2.0
INFO Uploading FW image firmwares/delta-patch.bin
INFO Uploaded FW image http://firmware-catalog-media-ca57.s3.dualstack.us-east-1.amazonaws.com/UttMp3crVuNntkxuNobTZI
INFO Vendor-ID: d3b2b23d842441739c666ee5cf74e594
INFO Class-ID: 90f4bdec6c0e483c8ecec3fbec8ba4fc
INFO Created manifest in v3 schema for delta update campaign
INFO Uploaded manifest ID: 017743762a0400000000000100100006
INFO Created Campaign ID: 017743762bb800000000000100100387
INFO Started Campaign ID: 017743762bb800000000000100100387
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

If you switch to the first terminal, notice in the device logs the downloading of the new firmware, the verification of the manifest and the successfull delta update: 

```
[FOTA INFO] fota.c:596: Firmware update initiated.
[FOTA DEBUG] fota.c:628: Pelion FOTA manifest is valid
[FOTA DEBUG] fota.c:651: get manifest : curr version 0, new version 131072 
[FOTA DEBUG] fota_source_profile_full.cpp:444: Reporting resource: /10252/0/2: value: 3
...
[FOTA DEBUG] fota.c:555: Download Authorization requested
[FOTA] ---------------------------------------------------
[FOTA] Updating component MAIN from version 0.0.0 to 0.2.0
[FOTA] Update priority 0
[FOTA] Delta update. Patch size 353657B full image size 6562160B
[FOTA] ---------------------------------------------------
[FOTA] Download authorization granted
...
[FOTA DEBUG] fota.c:1258: FOTA delta engine initialized
...
[FOTA] Downloading firmware. 3%
[FOTA] Downloading firmware. 9%
[FOTA] Downloading firmware. 11%
...
[FOTA] Downloading firmware. 100%
[FOTA INFO] fota.c:1509: Firmware download finished
[FOTA DEBUG] fota.c:1460: Install Authorization requested
[FOTA] Install authorization granted
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
...
```

This is also reflected in Pelion update campaign dashboard, showing the successfull completion of the update:

![alt text](https://i.ibb.co/bPyvFw8/portal-campaign-dashboard.png "Plus")

and the device displays the new firmware version (0.2.0 in our case):

![alt text](https://i.ibb.co/dp1fMYf/device-fw-version.png "Plus")