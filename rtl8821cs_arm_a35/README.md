# RTL8821CS SDIO EVM Testing

### Test Gear

|Test Board|SDIO EVM HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/73777836-d765-4618-8e4c-d843b326c991" height="400"/>|<img src="https://github.com/user-attachments/assets/ae6d6884-5310-426d-9a8c-f442d8d3f1b8" height="400"/>|

```
uname -r
6.1.111-rt42

cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

lscpu
Architecture:                         aarch64
CPU op-mode(s):                       32-bit, 64-bit
Byte Order:                           Little Endian
CPU(s):                               2
On-line CPU(s) list:                  0,1
Thread(s) per core:                   1
Core(s) per socket:                   2
Socket(s):                            1
Vendor ID:                            ARM
Model:                                0
Model name:                           Cortex-A35
Stepping:                             r1p0
BogoMIPS:                             66.66
Vulnerability Gather data sampling:   Not affected
Vulnerability Itlb multihit:          Not affected
Vulnerability L1tf:                   Not affected
Vulnerability Mds:                    Not affected
Vulnerability Meltdown:               Not affected
Vulnerability Mmio stale data:        Not affected
Vulnerability Reg file data sampling: Not affected
Vulnerability Retbleed:               Not affected
Vulnerability Spec rstack overflow:   Not affected
Vulnerability Spec store bypass:      Not affected
Vulnerability Spectre v1:             Mitigation; __user pointer sanitization
Vulnerability Spectre v2:             Not affected
Vulnerability Srbds:                  Not affected
Vulnerability Tsx async abort:        Not affected
Flags:                                fp asimd evtstrm aes pmull sha1 sha2 crc32
                                       cpuid
```

### SDIO Tree

Due to hardware limitation on the test gear SDIO only uses 3.3V.

So limited speed to <50MHz High-Speed Specification.

Reduce clock speed to 25MHz, which futher enhance bus stability as well.

Vendor driver had been tested and no issues are found compared with RTW88!

```
dmesg | grep mmc
[    0.000000] Kernel command line: console=ttyS0,115200n8 earlycon=uart,mmio32,0xf8401000 loglevel=8 root=/dev/mmcblk0p2 rootwait rootfstype=ext4 rw
[    0.936618] mmc0: SDHCI controller on f8049000.mmc [f8049000.mmc] using ADMA
[    0.941320] mmc1: SDHCI controller on f804a000.mmc [f804a000.mmc] using ADMA
[    0.941567] Waiting for root device /dev/mmcblk0p2...
[    0.965152] sdhci-dwcmshc f804a000.mmc: card claims to support voltages below defined range
[    1.081966] mmc0: new high speed SDHC card at address b368
[    1.082589] mmcblk0: mmc0:b368 NCard 29.1 GiB
[    1.085961]  mmcblk0: p1 p2
[    1.129662] EXT4-fs (mmcblk0p2): mounted filesystem with ordered data mode. Quota mode: disabled.
[    1.405198] mmc1: new high speed SDIO card at address 0001
[    4.823728] EXT4-fs (mmcblk0p2): re-mounted. Quota mode: disabled.
[    8.128178] FAT-fs (mmcblk0p1): Volume was not properly unmounted. Some data may be corrupt. Please run fsck.
[   42.746724] rtw_8821cs mmc1:0001:1: Firmware version 24.11.0, H2C version 12

MMC_TYPE=SDIO
SDIO_ID=024C:C821
SDIO_REVISION=0.0
clock:          25000000 Hz
actual clock:   25000000 Hz
vdd:            21 (3.3 ~ 3.4 V)
bus mode:       2 (push-pull)
chip select:    0 (don't care)
power mode:     2 (on)
bus width:      2 (4 bits)
timing spec:    2 (sd high-speed)
signal voltage: 0 (3.30 V)
driver type:    0 (driver type B)
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[   64.780916] rtw_core: loading out-of-tree module taints kernel.
[   65.594638] rtw_8821cs mmc1:0001:1: Firmware version 24.11.0, H2C version 12

lsmod
Module                  Size  Used by
rtw_8821cs             16384  0
rtw_8821c              94208  1 rtw_8821cs
rtw_sdio               20480  1 rtw_8821cs
rtw_core              217088  2 rtw_sdio,rtw_8821c
```
### Network Manager

Either nmcli nor nmtui connect to WIFI on STA mode will immediate trigger crash.

However reboot and insmod the driver again could not see any 

```
[  236.676378] skbuff: skb_over_panic: text:ffffffc000b16dfc len:1563 put:1563 head:ffffff8008a68e00 data:ffffff8008a68ed8 tail:0x6f3 end:0x440 dev:<NULL>
[  236.676461] ------------[ cut here ]------------
[  236.676464] kernel BUG at net/core/skbuff.c:120!
[  236.676472] Internal error: Oops - BUG: 00000000f2000800 [#1] PREEMPT SMP
[  236.705928] Modules linked in: rtw_8821cs(O) rtw_8821c(O) rtw_sdio(O) rtw_core(O)
[  236.713409] CPU: 0 PID: 142 Comm: kworker/0:3 Tainted: G           O       6.1.111-rt42 #14
[  236.721731] Hardware name: Anlogic, DR1M90 FPSoc (DT)
[  236.726765] Workqueue: events sdio_irq_work
[  236.730952] pstate: 40000005 (nZcv daif -PAN -UAO -TCO -DIT -SSBS BTYPE=--)
[  236.737890] pc : skb_panic+0x4c/0x50
[  236.741462] lr : skb_panic+0x4c/0x50
[  236.745030] sp : ffffff8002713bb0
[  236.748332] x29: ffffff8002713bc0 x28: 0000000000000000 x27: ffffff8008a69240
[  236.755454] x26: 0000000000000620 x25: ffffff80027d0200 x24: 000000000000001b
[  236.762576] x23: ffffff800c091e40 x22: 000000000000001b x21: 0000000000000319
[  236.769698] x20: ffffff8002713cd0 x19: ffffff8003798e00 x18: 0000000000000060
[  236.776819] x17: 0000000000000000 x16: 0000000000000000 x15: 3a61746164203030
[  236.783939] x14: 6538366138303038 x13: 554e3c3a76656420 x12: 30343478303a646e
[  236.791061] x11: 3e4c4c554e3c3a76 x10: 6564203034347830 x9 : 3a646e6520336636
[  236.798182] x8 : ffffffc008fd7ed8 x7 : ffffff80027139f0 x6 : ffffff801fe9f958
[  236.805303] x5 : ffffff801fe9f958 x4 : 0000000000000000 x3 : ffffff801fea2b88
[  236.812424] x2 : ffffff801fea2b88 x1 : ffffff8002183500 x0 : 000000000000008b
[  236.819545] Call trace:
[  236.821983]  skb_panic+0x4c/0x50
[  236.825207]  skb_put+0x74/0x78
[  236.828258]  rtw_sdio_rx_skb+0xbc/0xf8 [rtw_sdio]
[  236.832962]  rtw_sdio_rxfifo_recv+0x1d8/0x290 [rtw_sdio]
[  236.838268]  rtw_sdio_handle_interrupt+0x10c/0x190 [rtw_sdio]
[  236.844006]  process_sdio_pending_irqs+0x4c/0x180
[  236.848699]  sdio_irq_work+0x50/0x80
[  236.852268]  process_one_work+0x1fc/0x350
[  236.856273]  worker_thread+0x44/0x438
[  236.859929]  kthread+0x10c/0x118
[  236.863154]  ret_from_fork+0x10/0x20
[  236.866728] Code: a90023eb aa0a03e1 9126c120 940c6032 (d4210000)
[  236.872799] ---[ end trace 0000000000000000 ]---
[  236.872805] note: kworker/0:3[142] exited with irqs disabled
[  236.872853] note: kworker/0:3[142] exited with preempt_count 1
[  236.876444] ------------[ cut here ]------------
[  236.876457] WARNING: CPU: 0 PID: 0 at kernel/context_tracking.c:128 ct_kernel_exit.isra.6.constprop.8+0x98/0xa0
[  236.876489] Modules linked in: rtw_8821cs(O) rtw_8821c(O) rtw_sdio(O) rtw_core(O)
[  236.876523] CPU: 0 PID: 0 Comm: swapper/0 Tainted: G      D    O       6.1.111-rt42 #14
[  236.876536] Hardware name: Anlogic, DR1M90 FPSoc (DT)
[  236.876543] pstate: 200000c5 (nzCv daIF -PAN -UAO -TCO -DIT -SSBS BTYPE=--)
[  236.876555] pc : ct_kernel_exit.isra.6.constprop.8+0x98/0xa0
[  236.876567] lr : ct_idle_enter+0x10/0x20
[  236.876578] sp : ffffffc008fc3d80
[  236.876583] x29: ffffffc008fc3d80 x28: 0000000001215ff0 x27: 000000001ffbf8b8
[  236.876603] x26: 000000001ed02488 x25: 0000000000000072 x24: 0000000000000000
[  236.876622] x23: ffffffc009123000 x22: ffffff801fecbf00 x21: ffffffc008fc88e0
[  236.876642] x20: 0000000000000001 x19: ffffff801fea3e18 x18: 0000000000000000
[  236.876661] x17: 0000000000000000 x16: 0000000000000000 x15: fffffffe000c2480
[  236.876680] x14: 0000000000001000 x13: 00000000000000c3 x12: 0000000000000000
[  236.876698] x11: 0000000000000000 x10: 00000000000009e0 x9 : ffffffc008fc3d40
[  236.876718] x8 : ffffffc008fd0300 x7 : 0000000000000000 x6 : 00000001e4a33efb
[  236.876737] x5 : 00ffffffffffffff x4 : 4000000000000002 x3 : ffffffc008fc3d80
[  236.876756] x2 : 4000000000000000 x1 : ffffffc008ea8000 x0 : ffffffc008ea8e18
[  236.876775] Call trace:
[  236.876780]  ct_kernel_exit.isra.6.constprop.8+0x98/0xa0
[  236.876794]  ct_idle_enter+0x10/0x20
[  236.876805]  default_idle_call+0x20/0x6c
[  236.876821]  do_idle+0xf4/0x120
[  236.876837]  cpu_startup_entry+0x38/0x40
[  236.876851]  kernel_init+0x0/0x130
[  236.876862]  arch_post_acpi_subsys_init+0x0/0x18
[  236.876878]  start_kernel+0x634/0x658
[  236.876890]  __primary_switched+0xb4/0xbc
[  236.876901] ---[ end trace 0000000000000000 ]---
```

### Network Speed Test via Ookla

```
```

### Network Ping Tests

#### DNS-Ping

```
```

#### Self-Ping 

```
```

### iw list

<details>

<summary>iw list</summary>

```
iw list
Wiphy phy1
        max # scan SSIDs: 4
        max scan IEs length: 2243 bytes
        max # sched scan SSIDs: 0
        max # match sets: 0
        Retry short limit: 7
        Retry long limit: 4
        Coverage class: 0 (up to 0m)
        Device supports T-DLS.
        Supported Ciphers:
                * WEP40 (00-0f-ac:1)
                * WEP104 (00-0f-ac:5)
                * TKIP (00-0f-ac:2)
                * CCMP-128 (00-0f-ac:4)
                * CCMP-256 (00-0f-ac:10)
                * GCMP-128 (00-0f-ac:8)
                * GCMP-256 (00-0f-ac:9)
                * CMAC (00-0f-ac:6)
                * CMAC-256 (00-0f-ac:13)
                * GMAC-128 (00-0f-ac:11)
                * GMAC-256 (00-0f-ac:12)
        Available Antennas: TX 0x1 RX 0x1
        Configured Antennas: TX 0x1 RX 0x1
        Supported interface modes:
                 * IBSS
                 * managed
                 * AP
                 * AP/VLAN
                 * monitor
                 * P2P-client
                 * P2P-GO
        Band 1:
                Capabilities: 0x196e
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        RX STBC 1-stream
                        Max AMSDU length: 7935 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 2 usec (0x04)
                HT Max RX data rate: 150 Mbps
                HT TX/RX MCS rate indexes supported: 0-7, 32
                Bitrates (non-HT):
                        * 1.0 Mbps
                        * 2.0 Mbps
                        * 5.5 Mbps
                        * 11.0 Mbps
                        * 6.0 Mbps
                        * 9.0 Mbps
                        * 12.0 Mbps
                        * 18.0 Mbps
                        * 24.0 Mbps
                        * 36.0 Mbps
                        * 48.0 Mbps
                        * 54.0 Mbps
                Frequencies:
                        * 2412 MHz [1] (20.0 dBm)
                        * 2417 MHz [2] (20.0 dBm)
                        * 2422 MHz [3] (20.0 dBm)
                        * 2427 MHz [4] (20.0 dBm)
                        * 2432 MHz [5] (20.0 dBm)
                        * 2437 MHz [6] (20.0 dBm)
                        * 2442 MHz [7] (20.0 dBm)
                        * 2447 MHz [8] (20.0 dBm)
                        * 2452 MHz [9] (20.0 dBm)
                        * 2457 MHz [10] (20.0 dBm)
                        * 2462 MHz [11] (20.0 dBm)
                        * 2467 MHz [12] (20.0 dBm)
                        * 2472 MHz [13] (20.0 dBm)
                        * 2484 MHz [14] (disabled)
        Band 2:
                Capabilities: 0x196e
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        RX STBC 1-stream
                        Max AMSDU length: 7935 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 2 usec (0x04)
                HT Max RX data rate: 150 Mbps
                HT TX/RX MCS rate indexes supported: 0-7, 32
                VHT Capabilities (0x03d07122):
                        Max MPDU length: 11454
                        Supported Channel Width: neither 160 nor 80+80
                        short GI (80 MHz)
                        SU Beamformee
                        MU Beamformee
                        +HTC-VHT
                VHT RX MCS set:
                        1 streams: MCS 0-9
                        2 streams: not supported
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT RX highest supported: 390 Mbps
                VHT TX MCS set:
                        1 streams: MCS 0-9
                        2 streams: not supported
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT TX highest supported: 390 Mbps
                Bitrates (non-HT):
                        * 6.0 Mbps
                        * 9.0 Mbps
                        * 12.0 Mbps
                        * 18.0 Mbps
                        * 24.0 Mbps
                        * 36.0 Mbps
                        * 48.0 Mbps
                        * 54.0 Mbps
                Frequencies:
                        * 5180 MHz [36] (20.0 dBm) (radar detection)
                        * 5200 MHz [40] (20.0 dBm) (radar detection)
                        * 5220 MHz [44] (20.0 dBm) (radar detection)
                        * 5240 MHz [48] (20.0 dBm) (radar detection)
                        * 5260 MHz [52] (20.0 dBm) (radar detection)
                        * 5280 MHz [56] (20.0 dBm) (radar detection)
                        * 5300 MHz [60] (20.0 dBm) (radar detection)
                        * 5320 MHz [64] (20.0 dBm) (radar detection)
                        * 5500 MHz [100] (disabled)
                        * 5520 MHz [104] (disabled)
                        * 5540 MHz [108] (disabled)
                        * 5560 MHz [112] (disabled)
                        * 5580 MHz [116] (disabled)
                        * 5600 MHz [120] (disabled)
                        * 5620 MHz [124] (disabled)
                        * 5640 MHz [128] (disabled)
                        * 5660 MHz [132] (disabled)
                        * 5680 MHz [136] (disabled)
                        * 5700 MHz [140] (disabled)
                        * 5720 MHz [144] (disabled)
                        * 5745 MHz [149] (33.0 dBm)
                        * 5765 MHz [153] (33.0 dBm)
                        * 5785 MHz [157] (33.0 dBm)
                        * 5805 MHz [161] (33.0 dBm)
                        * 5825 MHz [165] (33.0 dBm)
        Supported commands:
                 * new_interface
                 * set_interface
                 * new_key
                 * start_ap
                 * new_station
                 * set_bss
                 * authenticate
                 * associate
                 * deauthenticate
                 * disassociate
                 * join_ibss
                 * remain_on_channel
                 * set_tx_bitrate_mask
                 * frame
                 * frame_wait_cancel
                 * set_wiphy_netns
                 * set_channel
                 * tdls_mgmt
                 * tdls_oper
                 * probe_client
                 * set_noack_map
                 * register_beacons
                 * start_p2p_device
                 * set_mcast_rate
                 * connect
                 * disconnect
                 * set_qos_map
                 * set_multicast_to_unicast
                 * Unknown command (140)
        software interface modes (can always be added):
                 * AP/VLAN
                 * monitor
        valid interface combinations:
                 * #{ managed } <= 1, #{ AP, P2P-client, P2P-GO } <= 1,
                   total <= 2, #channels <= 1
        HT Capability overrides:
                 * MCS: ff ff ff ff ff ff ff ff ff ff
                 * maximum A-MSDU length
                 * supported channel width
                 * short GI for 40 MHz
                 * max A-MPDU length exponent
                 * min MPDU start spacing
        Device supports TX status socket option.
        Device supports HT-IBSS.
        Device supports SAE with AUTHENTICATE command
        Device supports scan flush.
        Device supports per-vif TX power setting
        Driver supports full state transitions for AP/GO clients
        Driver supports a userspace MPM
        Device supports configuring vdev MAC-addr on create.
        Device supports randomizing MAC-addr in scans.
        max # scan plans: 1
        max scan plan interval: -1
        max scan plan iterations: 0
        Supported TX frame types:
                 * IBSS: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * managed: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * AP: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * AP/VLAN: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * mesh point: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * P2P-client: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * P2P-GO: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * P2P-device: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
        Supported RX frame types:
                 * IBSS: 0x40 0xb0 0xc0 0xd0
                 * managed: 0x40 0xb0 0xd0
                 * AP: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * AP/VLAN: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * mesh point: 0xb0 0xc0 0xd0
                 * P2P-client: 0x40 0xd0
                 * P2P-GO: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * P2P-device: 0x40 0xd0
        Supported extended features:
                * [ RRM ]: RRM
                * [ SET_SCAN_DWELL ]: scan dwell setting
                * [ FILS_STA ]: STA FILS (Fast Initial Link Setup)
                * [ CONTROL_PORT_OVER_NL80211 ]: control port over nl80211
                * [ TXQS ]: FQ-CoDel-enabled intermediate TXQs
```

</details>

### iwconfig

Once iwconfig command is given on the next boot and check the connection status.

Crash happened again!

```
wlan0     IEEE 802.11  ESSID:""
          Mode:Managed  Frequency:5.805 GHz  Access Point: 
          Bit Rate=117 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=40/70  Signal level=-70 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0


[  135.525797] skbuff: skb_over_panic: text:ffffffc000b16d98 len:754 put:754 head:ffffff80053e1400 data:ffffff80053e1440 tail:0x332 end:0x2c0 dev:<NULL>
[  135.525861] ------------[ cut here ]------------
[  135.525864] kernel BUG at net/core/skbuff.c:120!
[  135.525871] Internal error: Oops - BUG: 00000000f2000800 [#1] PREEMPT SMP
[  135.561045] Modules linked in: rtw_8821cs(O) rtw_8821c(O) rtw_sdio(O) rtw_core(O) [last unloaded: rtw_8821cs(O)]
[  135.571211] CPU: 0 PID: 16 Comm: kworker/0:1 Tainted: G           O       6.1.111-rt42 #14
[  135.579446] Hardware name: Anlogic, DR1M90 FPSoc (DT)
[  135.584478] Workqueue: events sdio_irq_work
[  135.588664] pstate: 40000005 (nZcv daif -PAN -UAO -TCO -DIT -SSBS BTYPE=--)
[  135.595603] pc : skb_panic+0x4c/0x50
[  135.599174] lr : skb_panic+0x4c/0x50
[  135.602743] sp : ffffff80000d7bb0
[  135.606046] x29: ffffff80000d7bc0 x28: 0000000000000000 x27: ffffff80053e160c
[  135.613167] x26: 0000000000000310 x25: ffffff8001efd000 x24: 0000000000000018
[  135.620289] x23: ffffff800b9c1e40 x22: 0000000000000018 x21: ffffff80000d7ca0
[  135.627410] x20: ffffff80000d7cd0 x19: ffffff8008a4cb00 x18: 0000000000000060
[  135.634530] x17: 000000000000763c x16: 0000000000000000 x15: 3a61746164203030
[  135.641651] x14: 3431653335303038 x13: 4c4c554e3c3a7665 x12: 642030633278303a
[  135.648772] x11: 3e4c4c554e3c3a76 x10: 6564203063327830 x9 : 3a646e6520323333
[  135.655894] x8 : ffffffc008fd7ed8 x7 : ffffff80000d79f0 x6 : ffffffc009087f30
[  135.663016] x5 : ffffff801fe9f958 x4 : 0000000000000000 x3 : 0000000000000027
[  135.670135] x2 : 0000000000000023 x1 : ffffff800009cf80 x0 : 0000000000000089
[  135.677257] Call trace:
[  135.679695]  skb_panic+0x4c/0x50
[  135.682920]  skb_put+0x74/0x78
[  135.685971]  rtw_sdio_rx_skb+0x58/0xf8 [rtw_sdio]
[  135.690675]  rtw_sdio_rxfifo_recv+0x1d8/0x290 [rtw_sdio]
[  135.695981]  rtw_sdio_handle_interrupt+0x10c/0x190 [rtw_sdio]
[  135.701719]  process_sdio_pending_irqs+0x4c/0x180
[  135.706412]  sdio_irq_work+0x50/0x80
[  135.709979]  process_one_work+0x1fc/0x350
[  135.713984]  worker_thread+0x44/0x438
[  135.717642]  kthread+0x10c/0x118
[  135.720867]  ret_from_fork+0x10/0x20
[  135.724441] Code: a90023eb aa0a03e1 9126c120 940c6032 (d4210000)
[  135.730513] ---[ end trace 0000000000000000 ]---
[  135.730519] note: kworker/0:1[16] exited with irqs disabled
[  135.730568] note: kworker/0:1[16] exited with preempt_count 1
[  135.738165] ------------[ cut here ]------------
[  135.738179] WARNING: CPU: 0 PID: 0 at kernel/context_tracking.c:128 ct_kernel_exit.isra.6.constprop.8+0x98/0xa0
[  135.738214] Modules linked in: rtw_8821cs(O) rtw_8821c(O) rtw_sdio(O) rtw_core(O) [last unloaded: rtw_8821cs(O)]
[  135.738253] CPU: 0 PID: 0 Comm: swapper/0 Tainted: G      D    O       6.1.111-rt42 #14
[  135.738265] Hardware name: Anlogic, DR1M90 FPSoc (DT)
[  135.738272] pstate: 200000c5 (nzCv daIF -PAN -UAO -TCO -DIT -SSBS BTYPE=--)
[  135.738284] pc : ct_kernel_exit.isra.6.constprop.8+0x98/0xa0
[  135.738296] lr : ct_idle_enter+0x10/0x20
[  135.738307] sp : ffffffc008fc3d80
[  135.738312] x29: ffffffc008fc3d80 x28: 0000000001215ff0 x27: 000000001ffbf8b8
[  135.738332] x26: 000000001ed02488 x25: 0000000000000072 x24: 0000000000000000
[  135.738351] x23: ffffffc009123000 x22: ffffff801fecbf00 x21: ffffffc008fc88e0
[  135.738371] x20: 0000000000000001 x19: ffffff801fea3e18 x18: 0000000000000000
[  135.738390] x17: 00000000000000c0 x16: 0000000000000020 x15: 0000000000000000
[  135.738409] x14: 00000000000000c9 x13: 00000000000000c9 x12: 0000000000000000
[  135.738427] x11: 0000000000000000 x10: 00000000000009e0 x9 : ffffffc008fc3d40
[  135.738446] x8 : ffffffc008fd0300 x7 : 0000000000000000 x6 : 000000011bb79dcd
[  135.738465] x5 : 00ffffffffffffff x4 : 4000000000000002 x3 : ffffffc008fc3d80
[  135.738484] x2 : 4000000000000000 x1 : ffffffc008ea8000 x0 : ffffffc008ea8e18
[  135.738504] Call trace:
[  135.738509]  ct_kernel_exit.isra.6.constprop.8+0x98/0xa0
[  135.738523]  ct_idle_enter+0x10/0x20
[  135.738534]  default_idle_call+0x20/0x6c
[  135.738550]  do_idle+0xf4/0x120
[  135.738566]  cpu_startup_entry+0x34/0x40
[  135.738581]  kernel_init+0x0/0x130
[  135.738592]  arch_post_acpi_subsys_init+0x0/0x18
[  135.738607]  start_kernel+0x634/0x658
[  135.738619]  __primary_switched+0xb4/0xbc
[  135.738630] ---[ end trace 0000000000000000 ]---
```

### Server & Client Test via iperf3 (PC-Router-DUT)

Cannot test due to driver crash!

<details>

<summary>iperf3</summary>

```
```

</details>

### AP Test

#### hostapd.conf

Setup the configuration at /etc/hostapd/hostapd.conf

```
interface=wlan0
driver=nl80211
ieee80211n=1
hw_mode=g
channel=6
ssid=AP-TEST
wpa=2
wpa_passphrase=12345678
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP TKIP
wpa_pairwise=TKIP CCMP
```

#### udhcpd.conf

```
start 192.168.175.2
end 192.168.175.254
interface wlan0
max_leases 234
opt router 192.168.175.1
```

#### Start AP Test
```
sudo hostapd -dd -e /dev/urandom /etc/hostapd/hostapd.conf -B
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr  and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

Cannot test due to driver crash!

<details>

<summary>iperf3</summary>

```
```

</details>
