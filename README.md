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

-   OpenCore 0.9.5
-   macOS Sonoma 14.0

Old macOS Versions:
-   macOS Ventura 13.5

## About upgrading to macOS Sonoma 14.0
No native support for BCM94360CS2, need to add some kexts and make some configurations. Links below may helps!

- [Sonoma 常遇到的問題（保持更新）](https://www.imacpc.net/archives/5324)
- [Hackintosh tutorial - Broadcom/Fenvi WIFI on MacOS Sonoma](https://www.youtube.com/watch?v=zHx2UIUsFuA)
- [OpenCore-Legacy-Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher) Get OCLP app & related kexts here!

Step summaries:

1. PATH: `NVRAM` - `ADD` - `7C436110-AB2A-4BBB-A880-FE41995C9F82`

- Add parameters in `boot-args`
   - `amfi=0x80`
   - `vsmcgen=1`
   - `-lilubetaall`
   - `vsmcbeta`
- Set `csr-active-config` to `03080000`

2. PATH: `NVRAM` - `DELETE` - `7C436110-AB2A-4BBB-A880-FE41995C9F82`

- Add `csr-active-config`

3. PATH: `MISC` - `Security` - `SecurityBootModel`

- Set to `Disabled`

4. `Kenel` - `Add` add `IOSkywalk.kext` & `IO80211FamilyLegacy.kext`（Min kernel version: `23.0.0`）

Add 3 kexts in order. 

5. `Kenel` - `Block` add `com.apple.iokit.IOSkywalkFamily` （Min kernel version: `23.0.0`） Strategy -> `Exclude`

6. Reboot your hackintosh

7. Download OCLP v1.0.1 and open this app, click `Post-Install Root Patch`, then `Start Root Patching`. 

8. After rebooting again, WiFi works.

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
