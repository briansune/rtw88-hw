# RTW88 Hardware Testing

### This repository is aim to provide RTW88 Community Driver Hardware Support Status

Test Version: [58638cb909377bed524ac9aad0ce7cefc1a037da](https://github.com/lwfinger/rtw88/tree/386382ace137f5209e8e83a4cf2e044bf52e8b38)

## iperf3 @ AP/STA test explain

Bluetooth speaker is used to trigger possible warning/error messages.

HOW TO DO: During the iperf3 test disconnect and reconnect the Bluetooth device and play music.

## Known Issue

2.4G WIFI band could be disturbed by nearby Bluetooth Devices and possible ZigBee Devices as well!

https://github.com/lwfinger/rtw88/issues/271#issuecomment-2566392845

## Issue found during testing

> I1: RTL8822BS is connected to merged 2.4G+5G Router.
> 
> Both 2.4G and 5G cannot connect under SDIO High-Speed Profile.

> I2: RTL8822BS is connected to splitted 2.4G+5G Router.
>
> 2.4G is able to connect under SDIO High-Speed Profile.

## SDIO Devices Investigation on RTW88

According to A35 DUT tested result.

DTS/DTSI device tree SDIO profile could introduce unstable issue on RTW88 or possible crashes.

All SDIO should first detected from low clock speed then enter high speed frequency ranges.

Most SDIO explain could be found [here](https://www.prodigytechno.com/sdio-protocol).

The current finding are as follows:

-> Low-Speed / High-Speed profile (4bits) is deployed with RTW88 driver

|Testbench|Device|Speed Profile|Issue|Vendor Driver|
|:---:|:---:|:---:|:---:|:---:|
|A35 ARM|RTL8723DS|Low-Speed|🟢|🟢|
|A35 ARM|RTL8821CS|Low-Speed|🔴 Crash on WIFI connection "Unable to Use"|🟢|
|A35 ARM|RTL8822BS|Low-Speed|⏳|❌ Support upto Kernel 5.4|
|A35 ARM|RTL8822CS|Low-Speed|🔴 Crash Message but no System Hang|🟢|
||||||
|A35 ARM|RTL8723DS|High-Speed|🟢|🟢|
|A35 ARM|RTL8821CS|High-Speed|⏳|🟢|
|A35 ARM|RTL8822BS|High-Speed|🟡 5G STA & AP Not Working|❌ Support upto Kernel 5.4|
|A35 ARM|RTL8822CS|High-Speed|🔴 Possible Network Drop |🟢|

## Fully RTW88 Driver Support Devices Test Report Table

|Phy Interface|<p>Chip #<p>HW Type|DUT Kernel #|Driver Tree|HW Image|Status|
|:---:|:---|:---|:---:|:---:|---:|
|<p>USB 2.0|<p>RTL8723 [D] U<p>Dongle|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8723x.ko<p>rtw_8723d.ko<p>rtw_8723du.ko|<p><img src="./images/8723du/rtl8723du_usb.png" width="200"/><p><img src="./images/8723du/rtl8723du_module.png" width="200"/>|<p>[ARM - A9 🟢](./rtl8723du_arm_a9)<p>[ARM64 - A35 🟡](./rtl8723du_arm_a35)<p>[ARM64 - A53 🟢](./rtl8723du_arm_a53)<p>STA 🟢<p>AP 🟡|
|||||||
|<p>USB 2.0|<p>RTL8811 [A] U<p>Dongle|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|rtw_core.ko<p>rtw_usb.ko<p>rtw_88xxa.ko<p>rtw_8821a.ko<p>rtw_8821au.ko|<img src="./images/8811au/rtl8811au_usb.png" width="200"/>|<p>[ARM - A9 🟡](./rtl8811au_arm_a9)<p>[ARM64 - A35 🟡](./rtl8811au_arm_a35)<p>[ARM64 - A53 🟡](./rtl8811au_arm_a53)<p>STA 🟡<p>AP 🔴|
|<p>USB 2.0|RTL8811 [C] U<p>Module|<p>5.4[ARM-A9]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8821c.ko<p>rtw_8821cu.ko|<img src="./images/8811cu/rtl8811cu_module.png" width="200"/>|<p>[ARM - A9 🟡](./rtl8811cu_arm_a9)<p>STA 🔴<p>AP 🟢|
|||||||
|<p>USB 2.0 (Only 2.4G)<p>USB 3.0 (HW Mod. 2.4G Only)|<p>RTL8812 [A] U<p>Dongle|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_88xxa.ko<p>rtw_8812a.ko<p>rtw_8812au.ko|<img src="./images/8812au/rtl8812au_usb.png" width="200"/>|<p>[ARM - A9 🟢](./rtl8812au_arm_a9)<p>[ARM64 - A35 🟡](./rtl8812au_arm_a35)<p>[ARM64 - A53 🟢](./rtl8812au_arm_a53)<p>[ARM64 - A53 USB 3.0 🟢](./rtl8812au_arm_a53_usb3)<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0<p>USB 3.0|<p>RTL8812 [A] U<p>USB PCBA|<p>6.1.111-rt42[ARM-A35]<p>5.4[ARM-A53]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_88xxa.ko<p>rtw_8812a.ko<p>rtw_8812au.ko|<img src="./images/8812au/rtl8812au_usb_5g.png" width="200"/>|<p>[ARM64 - A35 USB 2.0 🟢](./rtl8812au_arm_a35_usb2_5g)<p>[ARM64 - A53 USB 3.0 🟢](./rtl8812au_arm_a53_usb3_5g)<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0|<p>RTL8812 [B] U<p>USB PCBA|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822b.ko<p>rtw_8822bu.ko|<img src="./images/8812bu/rtl8812bu_pcba.png" width="200"/>|<p>[ARM - A9 🟢](./rtl8812bu_arm_a9)<p>[ARM64 - A35 🟡](./rtl8812bu_arm_a35)<p>[ARM64 - A53 🟢](./rtl8812bu_arm_a53)<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0|RTL8812 [C] U<p>USB PCBA|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822c.ko<p>rtw_8822cu.ko|<img src="./images/8812cu/rtl8812cu_pcba.JPG" width="200"/>|<p>ARM - A9 ⏳<p>[ARM64 - A35 🟢](./rtl8812cu_arm_a35)<p>[ARM64 - A53 🟢](./rtl8812cu_arm_a53)<p>STA 🟢<p>AP 🟡|
|||||||
|<p>USB 2.0|RTL8814 [A] U<p>USB PCBA|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8814a.ko<p>rtw_8814au.ko|<img src="./images/8814au/rtl8814au_pcba.png" width="200"/>|<p>[ARM - A9 🟡](./rtl8814au_arm_a9)<p>[ARM64 - A35 🟡](./rtl8814au_arm_a35)<p>[ARM64 - A53 🟡](./rtl8814au_arm_a53)<p>STA 🟢<p>AP 🟡|
|||||||
|<p>USB 2.0|RTL8821 [A] U<p>Module|<p>5.4[ARM-A9]||<img src="./images/8821au/rtl8821au_pcba.png" width="200"/>|<p>[ARM - A9 🟢](./rtl8821au_arm_a9)<p>ARM64 - A35 ⏳<p>ARM64 - A53 ⏳<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0|RTL8821 [C] U<p>Dongle|<p>5.4[ARM-A9]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8821c.ko<p>rtw_8821cu.ko|<p><img src="./images/8821cu/rtl8821cu_usb.png" width="200"/>|<p>[ARM - A9 🟡](./rtl8821cu_arm_a9)<p>ARM64 - A35 ⏳<p>[ARM64 - A53 🟢](./rtl8821cu_arm_a53)<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0|RTL8821 [C] U<p>Dongle|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8821c.ko<p>rtw_8821cu.ko|<p><img src="./images/8821cu/rtl8821cu_pcba.png" width="200"/>|<p>[ARM - A9 🟡](./rtl8821cu_arm_a9_pcba)<p>STA 🟡<p>AP ⏳|
|||||||
|<p>USB 2.0<p>USB 3.0|RTL8822 [B] U<p>Dongle|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822b.ko<p>rtw_8822bu.ko|<img src="./images/8822bu/rtl8822bu_usb.png" width="200"/>|<p>[ARM - A9 🟢](./rtl8822bu_arm_a9)<p>ARM64 - A35 🟡<p>[ARM64 - A53 🟡](./rtl8822bu_arm_a53)<p>STA 🟢<p>AP 🟡||
|<p>USB 2.0|RTL8822 [C] U<p>Module|<p>5.4[ARM-A9/53]<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822c.ko<p>rtw_8822cu.ko|<img src="./images/8822cu/rtl8822cu_module.JPG" width="200"/>|<p>ARM - A9 ⏳<p>[ARM - A35 🟢](./rtl8822cu_arm_a35)<p>ARM - A53 ⏳<p>STA 🟢<p>AP 🟢|
|||||||
|SDIO|RTL8723 [D] S<p>Custom HW|<p>5.4[ARM-A9/53]|<p>rtw_core.ko<p>rtw_sdio.ko<p>rtw_8723x.ko<p>rtw_8723d.ko<p>rtw_8723ds.ko|<img src="./images/8723ds/rtl8723ds_custom.JPG" width="200"/>|<p>ARM - A9 🟢<p>STA ⏳<p>AP ⏳|
|SDIO|RTL8723 [D] S<p>Module HW|<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_sdio.ko<p>rtw_8723x.ko<p>rtw_8723d.ko<p>rtw_8723ds.ko|<img src="./images/8723ds/rtl8723ds_pcba.JPG" width="200"/>|<p>ARM64 - A35 🟡<p>STA ⏳<p>AP ⏳|
|||||||
|SDIO|RTL8821 [C] S<p>PCBA EVM|<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_sdio.ko<p>rtw_8821c.ko<p>rtw_8821cs.ko|<img src="./images/8821cs/rtl8821cs_module.png" width="200"/>|<p>[ARM - A35 🔴](./rtl8821cs_arm_a35)<p>STA 🔴<p>AP 🔴|
|||||||
|SDIO|RTL8822 [B] S<p>PCBA EVM|<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_sdio.ko<p>rtw_8822b.ko<p>rtw_8822bs.ko|<img src="./images/8822bs/rtl8822bs_module.png" width="200"/>|<p>[ARM - A35 (High-Speed) 🟡](./rtl8822bs_arm_a35)<p>STA 🟡<p>AP 🔴|
|SDIO|RTL8822 [C] S<p>PCBA EVM|<p>6.1.111-rt42[ARM-A35]|<p>rtw_core.ko<p>rtw_sdio.ko<p>rtw_8822c.ko<p>rtw_8822cs.ko|<img src="./images/8822cs/rtl8822cs_pcba.png" width="200"/>|⏳|
|||||||
|PCIe|RTL8723 [D] E<p>M.2 Card|<p>5.4[ARM-A53]|<p>rtw_core.ko|<img src="./images/8723de/rtl8723de_m2card.JPG" width="200"/>|⏳|
|||||||
|PCIe|RTL8821 [C] E<p>M.2 Card|<p>5.4[ARM-A53]|<p>rtw_core.ko|<img src="./images/8821ce/rtl8821ce_m2card.JPG" width="200"/>|⏳|
|||||||
|PCIe|RTL8822 [B] E<p>M.2 Card|<p>5.4[ARM-A53]|<p>rtw_core.ko|<img src="./images/8822be/rtl8822be_m2card.JPG" width="200"/>|⏳|
|PCIe|RTL8822 [C] E<p>M.2 Card|<p>5.4[ARM-A53]|<p>rtw_core.ko|<img src="./images/8822ce/rtl8822ce_m2card.JPG" width="200"/>|⏳|

