I have been used this machine as a hackintosh for developing since Nov. 2020, for almost 3 years! The longest up time was 40 days because of locking down of Covid-19, and it worked fine when I returned without rebooting. Pretty stable!

Saddly found that the compile speed difference of my project(golang) between this hackintosh and M2 Pro MBP was large, and obviously M2 Pro compiles much faster. Here are their compile tests for the same code(including handling vendors & dependencies)

-   In this hackintosh: 

    ```shell
    $ /usr/bin/time -h make all
    ...
            1m15.64s real           8m24.56s user           1m40.72s sys
    ```

-   In M2 Pro MBP

    ```shell
    $ /usr/bin/time -h make all
    ...
            37.17s real             3m46.23s user           39.77s sys
    ```

## Hardwares

| Item                   | Detail                        |
| ---------------------- | ----------------------------- |
| Motherboard            | ASRock Deskmini H470          |
| CPU                    | i5-10500                      |
| iGPU                   | UHD 630                       |
| WiFi & Blutooth（M.2） | BCM94360CS2                   |
| Memory                 | Kinston DDR4 3200MHz 16GB x 2 |
| Storages               | M.2 SSD x 1                   |
| BIOS Version           |                               |

## Current Version

-   OpenCore 0.9.3
-   macOS Ventura 13.5

## Works fine

-   Start and shutdown
-   App Store login and download
-   iCloud,iMessage,AirDrop
-   WiFi, Bluetooth, Ethernet

## Known Issues

-   File Share can't be opened from preference

## BIOS Settings

The BIOS I set before was **missing**, but it's pretty simple and just need to do few settings. So you can try the following configurations below if it doesn't works.

-   **Secure Boot : Disabled**
-   **Internal Graphics : Disabled**
-   Above 4G Decoding : Enabled
-   Above 4GB MMIO BIOS assignment : Enabled
-   Re-Size BAR Support : Disabled
-   **Intel Platform Trust Technology(PTT): Disabled**
-   **Hyper-Threading : Enabled**
-   **CFG Lock : Disabled**

------

-   Fast Boot - Disabled
-   CSM - Disabled
-   VT-d, Thunderbolt - Disabled
-   Serial port - Disabled
-   Intel SGX - Disabled

------

-   OS type: Other OS
-   EHCI/XHCI Hand-off - Enabled
-   Security Device Support - Disable
-   Internal Graphics - Disabled

## What to do next?

-   Generate model information after selecting ` iMac20,1` aka `iMac (Retina 5K, 27-inch, 2020)`.
-   Hope your hackintosh come to you as soon as possibile and have a good night!

## Other things may help

-   Reset NVRAM after changing EFI

## Key shots about this motherboard

| Key Shot | Functionality                      |
| -------- | ---------------------------------- |
| Del      | Get into BIOS Setup                |
| F12      | Select bootloader to start         |
| F10      | Save & Quit                        |
| F2       | Change to Advanced Mode in BIOS UI |
