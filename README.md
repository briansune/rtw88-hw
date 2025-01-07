# RTW88 Hardware Testing

## This repository is aim to provide RTW88 Community Driver Hardware Support Status

## Latest RTW88 Driver Support List


|Phy Interface|Chip #|HW Type|Driver Tree|HW Image|Status|
|:---:|:---|:---|:---:|:---:|---:|
|<p>USB 2.0|RTL8723 [D] U|Dongle|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8723x.ko<p>rtw_8723d.ko<p>rtw_8723du.ko|<p><img src="https://github.com/user-attachments/assets/7570044c-ef8e-49a7-9159-3d2053ef6aa1" width="200"/><p><img src="https://github.com/user-attachments/assets/2de36784-24e9-4c18-8ebd-92ce5fbc8eed" width="200"/>|<p>[ARM - A9 🟢](./rtl8723du_arm_a9)<p>[ARM64 - A35 🟡](./rtl8723du_arm_a35)<p>[ARM64 - A53 🟢](./rtl8723du_arm_a53)<p>STA 🟢<p>AP 🟡|
|||||||
|<p>USB 2.0|RTL8811 [A] U|Dongle|rtw_core.ko<p>rtw_usb.ko<p>rtw_88xxa.ko<p>rtw_8821a.ko<p>rtw_8821au.ko|<img src="https://github.com/user-attachments/assets/7efc5f62-b470-47ac-85c2-8372cbe51a69" width="200"/>|<p>[ARM - A9 🟡](./rtl8811au_arm_a9)<p>[ARM64 - A35 🟡](./rtl8811au_arm_a35)<p>ARM64 - A53 ⏳<p>STA 🟡<p>AP 🔴|
|<p>USB 2.0|RTL8811 [C] U|Module||<img src="https://github.com/user-attachments/assets/57dc7d6e-8fc9-4008-b1a5-83038d3afb6a" width="200"/>|<p>[ARM - A9 🟡](./rtl8811cu_arm_a9)<p>ARM64 - A35 ✖<p>ARM64 - A53 ✖<p>STA 🔴<p>AP 🟢|
|||||||
|<p>USB 2.0 (Only 2.4G)<p>USB 3.0 (HW Mod. 2.4G Only)|RTL8812 [A] U|Dongle|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_88xxa.ko<p>rtw_8812a.ko<p>rtw_8812au.ko|<img src="https://github.com/user-attachments/assets/f4c05105-5f9e-4de4-b3b5-8a3cbd5bb22f" width="200"/>|<p>[ARM - A9 🟢](./rtl8812au_arm_a9)<p>[ARM64 - A35 🟡](./rtl8812au_arm_a35)<p>[ARM64 - A53 🟢](./rtl8812au_arm_a53)<p>[ARM64 - A53 USB 3.0 🟢](./rtl8812au_arm_a53_usb3)<p>STA 🟢<p>AP 🟡|
|<p>USB 3.0|RTL8812 [A] U|USB PCBA|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_88xxa.ko<p>rtw_8812a.ko<p>rtw_8812au.ko|<img src="https://github.com/user-attachments/assets/b1ec9a82-48ca-4745-8aee-fc0e5e6b7c4a" width="200"/>|<p>[ARM64 - A53 USB 3.0 🟢](./rtl8812au_arm_a53_usb3_5g)<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0|RTL8812 [B] U|USB PCBA|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822b.ko<p>rtw_8822bu.ko|<img src="https://github.com/user-attachments/assets/eeabb9c2-c26c-41d2-98cb-55698a9cc437" width="200"/>|<p>ARM - A9 ⏳<p>ARM64 - A35 ⏳<p>[ARM64 - A53 🟢](./rtl8812bu_arm_a53)<p>STA 🟢<p>AP 🟢|
|<p>USB 2.0|RTL8812 [C] U|USB PCBA|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822c.ko<p>rtw_8822cu.ko|<img src="https://github.com/user-attachments/assets/efad8c56-5be0-4683-840b-530aa36a3f4d" width="200"/>|<p>ARM - A9 ⏳<p>ARM64 - A35 ⏳<p>[ARM64 - A53 🟢](./rtl8812cu_arm_a53)<p>STA 🟢<p>AP 🟢|
|||||||
|<p>USB 2.0|RTL8814 [A] U|USB PCBA|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8814a.ko<p>rtw_8814au.ko|<img src="https://github.com/user-attachments/assets/caaf1a45-e727-49c7-9f23-68beabce392b" width="200"/>|<p>ARM - A9 ⏳<p>ARM64 - A35 ⏳<p>[ARM64 - A53 🟡](./rtl8814au_arm_a53)<p>STA 🟢<p>AP 🟡|
|||||||
|<p>USB 2.0|RTL8821 [A] U||||✖|
|<p>USB 2.0|RTL8821 [C] U|Dongle|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8821c.ko<p>rtw_8821cu.ko|<p><img src="https://github.com/user-attachments/assets/20a5b758-1305-4ba6-944b-3f32485f26a9" width="200"/>|<p>[ARM - A9 🟡](./rtl8821cu_arm_a9)<p>ARM64 - A35 ⏳<p>[ARM64 - A53 🟢](./rtl8821cu_arm_a53)<p>STA 🟢<p>AP 🟡|
|<p>USB 2.0|RTL8821 [C] U|Dongle|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8821c.ko<p>rtw_8821cu.ko|<p><img src="https://github.com/user-attachments/assets/3b42204e-2e0c-46d8-ae13-adcf35eb7017" width="200"/>|<p>[ARM - A9 🟡](./rtl8821cu_arm_a9_pcba)<p>STA 🟡<p>AP ⏳|
|||||||
|<p>USB 2.0<p>USB 3.0|RTL8822 [B] U|Dongle|<p>rtw_core.ko<p>rtw_usb.ko<p>rtw_8822b.ko<p>rtw_8822bu.ko|<img src="https://github.com/user-attachments/assets/06b10ca5-1407-4069-b684-19f6bb726662" width="200"/>|<p>[ARM - A9 🟢](./rtl8822bu_arm_a9)<p>ARM64 - A35 🟡<p>[ARM64 - A53 🟡](./rtl8822bu_arm_a53)<p>STA 🟢<p>AP 🟡||
|<p>USB 2.0|RTL8822 [C] U||||✖|
|||||||
|SDIO|RTL8723 [D] S|Custom HW|<p>rtw_core.ko<p>rtw_sdio.ko<p>rtw_8723x.ko<p>rtw_8723d.ko<p>rtw_8723ds.ko|<img src="https://github.com/user-attachments/assets/13eda78d-f579-4ec6-9320-2d4821633a1b" width="200"/>|<p>ARM - A9 🟢<p>ARM64 - A35 🟡<p>ARM64 - A53 ⏳<p>STA ⏳<p>AP ⏳|
|||||||
|SDIO|RTL8821 [C] S|Module||<img src="https://github.com/user-attachments/assets/23521524-ab58-40be-9028-dd850306dc1b" width="200"/>|⏳|
|||||||
|SDIO|RTL8822 [B] S|Module||<img src="https://github.com/user-attachments/assets/a93f93ed-912f-4993-a39c-5b3bdd804f6e" width="200"/>|⏳|
|SDIO|RTL8822 [C] S|Module||<img src="https://github.com/user-attachments/assets/105c7116-77f7-4693-a3a6-09583535debd" width="200"/>|⏳|


