# RTL8811AU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/6b0e7499-aaa1-461e-b9cc-a19852c82370" height="400"/>|<img src="https://github.com/user-attachments/assets/e33d820c-4b2a-42e0-8a23-474676784b78" height="400"/>|

```
uname -r
6.1.111-rt42

lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.2 LTS
Release:        20.04
Codename:       focal

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

### USB Tree

```
Before driver loaded
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Vendor Specific Class, Driver=, 480M

After driver loaded
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Vendor Specific Class, Driver=rtw_8821au, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 002: ID 0bda:0811 Realtek Semiconductor Corp. 802.11n WLAN Adapter
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0x0811
  bcdDevice            2.00
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength       0x003c
    bNumInterfaces          1
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0x80
      (Bus Powered)
    MaxPower              500mA
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           6
      bInterfaceClass       255 Vendor Specific Class
      bInterfaceSubClass    255 Vendor Specific Subclass
      bInterfaceProtocol    255 Vendor Specific Protocol
      iInterface              2
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x84  EP 4 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x05  EP 5 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x06  EP 6 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x87  EP 7 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               3
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x08  EP 8 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x09  EP 9 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[  110.052716] rtw_core: loading out-of-tree module taints kernel.
[  132.999083] rtw_8821au 1-1:1.0: Firmware version 42.4.0, H2C version 0
[  133.495228] rtw_8821au 1-1:1.0: efuse MAC invalid, using random
[  133.510456] usbcore: registered new interface driver rtw_8821au

Module                  Size  Used by
rtw_8821au             16384  0
rtw_8821a              36864  1 rtw_8821au
rtw_88xxa              36864  1 rtw_8821a
rtw_usb                24576  1 rtw_8821au
rtw_core              217088  3 rtw_88xxa,rtw_usb,rtw_8821a
```

### Network Manager

When connecting to the router (STA), nmtui will stuck and need to remove and reconnect to achieve connection.

```
[  216.938119] wlan0: authenticate with 
[  218.073209] wlan0: send auth to  (try 1/3)
[  218.115719] wlan0: send auth to  (try 2/3)
[  218.127844] wlan0: authenticated
[  218.132286] wlan0: associate with  (try 1/3)
[  218.208354] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  218.216767] wlan0: associated
[  218.234597] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  221.233183] wlan0: deauthenticated from  (Reason: 15=4WAY_HANDSHAKE_TIMEOUT)
[  268.245722] wlan0: authenticate with 
[  269.511605] wlan0: send auth to  (try 1/3)
[  269.524988] wlan0: send auth to  (try 2/3)
[  269.538786] wlan0: send auth to  (try 3/3)
[  269.552105] wlan0: authentication with  timed out
[  274.442571] wlan0: authenticate with 
[  275.561165] wlan0: send auth to  (try 1/3)
[  275.568295] wlan0: authenticated
[  275.580300] wlan0: associate with  (try 1/3)
[  275.704253] wlan0: associate with  (try 2/3)
[  275.707492] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  275.716135] wlan0: associated
[  275.985952] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[  275.991184] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  279.938833] efuse thermal meter is 0xff


wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.33  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 84  bytes 10236 (10.2 KB)
        RX errors 0  dropped 9  overruns 0  frame 0
        TX packets 40  bytes 6859 (6.8 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

[error] Error: [0] Timeout occurred in connect.
[error] Error: [0] Cannot open socket
[error] Error: [0] Cannot open socket
[error] Error: [0] Cannot open socket
[error] Error: [0] Cannot open socket
[error] Error: [0] Cannot open socket
[error] Error: [0] Cannot read from socket:
[error] Error: [0] Timeout occurred in connect.
[error] Error: [0] Timeout occurred in connect.
[error] Error: [0] Cannot read from socket:
[error] Server Selection - Failed to find a working test server. (NoServers)
```
### Network Ping Tests

#### DNS-Ping

Ping connect complete STA is having issue!

```
[  275.985952] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[  275.991184] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  279.938833] efuse thermal meter is 0xff
[  571.165074] wlan0: authenticate with 
[  572.310928] wlan0: send auth to  (try 1/3)
[  572.336244] wlan0: authenticated
[  572.340267] wlan0: associate with  (try 1/3)
[  572.405015] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  572.413488] wlan0: associated
[  572.534748] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  938.940407] wlan0: deauthenticating from  by local choice (Reason: 3=DEAUTH_LEAVING)
[  960.109882] wlan0: authenticate with 
[  961.291509] wlan0: send auth to  (try 1/3)
[  961.304700] wlan0: send auth to  (try 2/3)
[  961.317624] wlan0: send auth to  (try 3/3)
[  961.330437] wlan0: authentication with  timed out
[  966.273499] wlan0: authenticate with 
[  967.469595] wlan0: send auth to  (try 1/3)
[  967.482495] wlan0: send auth to  (try 2/3)
[  967.495401] wlan0: send auth to  (try 3/3)
[  967.508440] wlan0: authentication with  timed out
[  982.627376] wlan0: authenticate with 
[  983.758129] wlan0: send auth to  (try 1/3)
[  983.762982] wlan0: authenticated
[  983.769423] wlan0: associate with  (try 1/3)
[  983.800490] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  983.809423] wlan0: associated
[  983.810014] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[  983.870670] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 


PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=37.0 ms
From 192.168.1.33 icmp_seq=4 Destination Host Unreachable
From 192.168.1.33 icmp_seq=5 Destination Host Unreachable
From 192.168.1.33 icmp_seq=6 Destination Host Unreachable
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=1595 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=271 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=74.2 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=8.13 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=43.9 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=127 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=185 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=95.6 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=116 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 10 received, +3 errors, 50% packet loss, time 19206ms
rtt min/avg/max/mdev = 8.125/255.271/1594.810/452.428 ms, pipe 3
```

#### Self-Ping 

```
PING 192.168.1.33 (192.168.1.33) 10000(10028) bytes of data.
10008 bytes from 192.168.1.33: icmp_seq=1 ttl=64 time=0.129 ms
10008 bytes from 192.168.1.33: icmp_seq=2 ttl=64 time=0.096 ms
10008 bytes from 192.168.1.33: icmp_seq=3 ttl=64 time=0.138 ms
10008 bytes from 192.168.1.33: icmp_seq=4 ttl=64 time=0.127 ms
10008 bytes from 192.168.1.33: icmp_seq=5 ttl=64 time=0.077 ms
10008 bytes from 192.168.1.33: icmp_seq=6 ttl=64 time=0.083 ms
10008 bytes from 192.168.1.33: icmp_seq=7 ttl=64 time=0.071 ms
10008 bytes from 192.168.1.33: icmp_seq=8 ttl=64 time=0.107 ms
10008 bytes from 192.168.1.33: icmp_seq=9 ttl=64 time=0.075 ms
10008 bytes from 192.168.1.33: icmp_seq=10 ttl=64 time=0.088 ms
10008 bytes from 192.168.1.33: icmp_seq=11 ttl=64 time=0.077 ms
10008 bytes from 192.168.1.33: icmp_seq=12 ttl=64 time=0.070 ms
10008 bytes from 192.168.1.33: icmp_seq=13 ttl=64 time=0.094 ms
10008 bytes from 192.168.1.33: icmp_seq=14 ttl=64 time=0.119 ms
10008 bytes from 192.168.1.33: icmp_seq=15 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.33: icmp_seq=16 ttl=64 time=0.080 ms
10008 bytes from 192.168.1.33: icmp_seq=17 ttl=64 time=0.071 ms
10008 bytes from 192.168.1.33: icmp_seq=18 ttl=64 time=0.090 ms
10008 bytes from 192.168.1.33: icmp_seq=19 ttl=64 time=0.086 ms
10008 bytes from 192.168.1.33: icmp_seq=20 ttl=64 time=0.103 ms

--- 192.168.1.33 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19462ms
rtt min/avg/max/mdev = 0.070/0.096/0.146/0.023 ms
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy0
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
                Minimum RX AMPDU time spacing: 16 usec (0x07)
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
                        * 2467 MHz [12] (20.0 dBm) (no IR)
                        * 2472 MHz [13] (20.0 dBm) (no IR)
                        * 2484 MHz [14] (20.0 dBm) (no IR)
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
                Minimum RX AMPDU time spacing: 16 usec (0x07)
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
                        * 5180 MHz [36] (20.0 dBm) (no IR)
                        * 5200 MHz [40] (20.0 dBm) (no IR)
                        * 5220 MHz [44] (20.0 dBm) (no IR)
                        * 5240 MHz [48] (20.0 dBm) (no IR)
                        * 5260 MHz [52] (20.0 dBm) (no IR, radar detection)
                        * 5280 MHz [56] (20.0 dBm) (no IR, radar detection)
                        * 5300 MHz [60] (20.0 dBm) (no IR, radar detection)
                        * 5320 MHz [64] (20.0 dBm) (no IR, radar detection)
                        * 5500 MHz [100] (20.0 dBm) (no IR, radar detection)
                        * 5520 MHz [104] (20.0 dBm) (no IR, radar detection)
                        * 5540 MHz [108] (20.0 dBm) (no IR, radar detection)
                        * 5560 MHz [112] (20.0 dBm) (no IR, radar detection)
                        * 5580 MHz [116] (20.0 dBm) (no IR, radar detection)
                        * 5600 MHz [120] (20.0 dBm) (no IR, radar detection)
                        * 5620 MHz [124] (20.0 dBm) (no IR, radar detection)
                        * 5640 MHz [128] (20.0 dBm) (no IR, radar detection)
                        * 5660 MHz [132] (20.0 dBm) (no IR, radar detection)
                        * 5680 MHz [136] (20.0 dBm) (no IR, radar detection)
                        * 5700 MHz [140] (20.0 dBm) (no IR, radar detection)
                        * 5720 MHz [144] (20.0 dBm) (no IR, radar detection)
                        * 5745 MHz [149] (20.0 dBm) (no IR)
                        * 5765 MHz [153] (20.0 dBm) (no IR)
                        * 5785 MHz [157] (20.0 dBm) (no IR)
                        * 5805 MHz [161] (20.0 dBm) (no IR)
                        * 5825 MHz [165] (20.0 dBm) (no IR)
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

```
wlan0     IEEE 802.11  ESSID:""
          Mode:Managed  Frequency:2.412 GHz  Access Point: 
          Bit Rate=27 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=50/70  Signal level=-60 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:74   Missed beacon:0
```

### Server & Client Test via iperf3 (PC-Router-DUT)

iperf3 cannot work, dead!

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.32, port 59844
[  5] local 192.168.1.33 port 5201 connected to 192.168.1.32 port 59846
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   140 KBytes  1.14 Mbits/sec    1   14.3 KBytes
[  5]   1.00-2.00   sec  0.00 Bytes  0.00 bits/sec    0   14.3 KBytes
[  5]   2.00-3.00   sec  0.00 Bytes  0.00 bits/sec    0   14.3 KBytes
[  5]   3.00-4.00   sec  0.00 Bytes  0.00 bits/sec    0   14.3 KBytes
[  5]   4.00-5.00   sec  0.00 Bytes  0.00 bits/sec    1   1.43 KBytes
[  5]   5.00-6.00   sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]   6.00-7.00   sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]   7.00-8.00   sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]   8.00-9.00   sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]   9.00-10.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  10.00-11.00  sec  0.00 Bytes  0.00 bits/sec    1   1.43 KBytes
[  5]  11.00-12.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  12.00-13.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  13.00-14.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  14.00-15.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  15.00-16.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  16.00-17.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  17.00-18.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  18.00-19.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  19.00-20.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  20.00-21.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  21.00-22.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  21.00-22.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-22.00  sec   140 KBytes  52.0 Kbits/sec    3             sender
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
sudo hostapd /etc/hostapd/hostapd.conf -B
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr  and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

Both ping and iperf3 cannot work.

<details>

<summary>dmesg</summary>

```
[  216.938119] wlan0: authenticate with 
[  218.073209] wlan0: send auth to  (try 1/3)
[  218.115719] wlan0: send auth to  (try 2/3)
[  218.127844] wlan0: authenticated
[  218.132286] wlan0: associate with  (try 1/3)
[  218.208354] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  218.216767] wlan0: associated
[  218.234597] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  221.233183] wlan0: deauthenticated from  (Reason: 15=4WAY_HANDSHAKE_TIMEOUT)
[  268.245722] wlan0: authenticate with 
[  269.511605] wlan0: send auth to  (try 1/3)
[  269.524988] wlan0: send auth to  (try 2/3)
[  269.538786] wlan0: send auth to  (try 3/3)
[  269.552105] wlan0: authentication with  timed out
[  274.442571] wlan0: authenticate with 
[  275.561165] wlan0: send auth to  (try 1/3)
[  275.568295] wlan0: authenticated
[  275.580300] wlan0: associate with  (try 1/3)
[  275.704253] wlan0: associate with  (try 2/3)
[  275.707492] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  275.716135] wlan0: associated
[  275.985952] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[  275.991184] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  279.938833] efuse thermal meter is 0xff
[  571.165074] wlan0: authenticate with 
[  572.310928] wlan0: send auth to  (try 1/3)
[  572.336244] wlan0: authenticated
[  572.340267] wlan0: associate with  (try 1/3)
[  572.405015] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  572.413488] wlan0: associated
[  572.534748] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  938.940407] wlan0: deauthenticating from  by local choice (Reason: 3=DEAUTH_LEAVING)
[  960.109882] wlan0: authenticate with 
[  961.291509] wlan0: send auth to  (try 1/3)
[  961.304700] wlan0: send auth to  (try 2/3)
[  961.317624] wlan0: send auth to  (try 3/3)
[  961.330437] wlan0: authentication with  timed out
[  966.273499] wlan0: authenticate with 
[  967.469595] wlan0: send auth to  (try 1/3)
[  967.482495] wlan0: send auth to  (try 2/3)
[  967.495401] wlan0: send auth to  (try 3/3)
[  967.508440] wlan0: authentication with  timed out
[  982.627376] wlan0: authenticate with 
[  983.758129] wlan0: send auth to  (try 1/3)
[  983.762982] wlan0: authenticated
[  983.769423] wlan0: associate with  (try 1/3)
[  983.800490] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=5)
[  983.809423] wlan0: associated
[  983.810014] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[  983.870670] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[ 1036.050399] rtw_8821au 1-1:1.0: firmware failed to leave lps state
[ 1053.917304] wlan0: deauthenticating from  by local choice (Reason: 3=DEAUTH_LEAVING)
[ 1075.213866] wlan0: authenticate with 
[ 1076.440581] wlan0: send auth to  (try 1/3)
[ 1076.453753] wlan0: send auth to  (try 2/3)
[ 1076.466777] wlan0: send auth to  (try 3/3)
[ 1076.479528] wlan0: authentication with  timed out
[ 1081.400747] wlan0: authenticate with 
[ 1082.619672] wlan0: send auth to  (try 1/3)
[ 1082.632694] wlan0: send auth to  (try 2/3)
[ 1082.646082] wlan0: send auth to  (try 3/3)
[ 1082.659047] wlan0: authentication with  timed out
[ 1087.964826] wlan0: authenticate with 
[ 1089.127874] wlan0: send auth to  (try 1/3)
[ 1089.146571] wlan0: authenticated
[ 1089.148965] wlan0: associate with  (try 1/3)
[ 1089.247849] wlan0: associate with  (try 2/3)
[ 1089.345483] wlan0: associate with  (try 3/3)
[ 1089.435010] wlan0: association with  timed out
[ 1094.721494] wlan0: authenticate with 
[ 1095.944920] wlan0: send auth to  (try 1/3)
[ 1095.958621] wlan0: send auth to  (try 2/3)
[ 1095.971785] wlan0: send auth to  (try 3/3)
[ 1095.984929] wlan0: authentication with  timed out
[ 1098.096211] wlan0: authenticate with 
[ 1099.220195] wlan0: send auth to  (try 1/3)
[ 1099.241572] wlan0: authenticated
[ 1099.243515] wlan0: associate with  (try 1/3)
[ 1099.299330] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=2)
[ 1099.307845] wlan0: associated
[ 1099.307875] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[ 1099.683697] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[ 1145.191352] wlan0: deauthenticating from  by local choice (Reason: 3=DEAUTH_LEAVING)
[ 1150.543519] wlan0: authenticate with 
[ 1151.663160] wlan0: send auth to  (try 1/3)
[ 1151.703924] wlan0: authenticated
[ 1151.706780] wlan0: associate with  (try 1/3)
[ 1151.796996] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=2)
[ 1151.805472] wlan0: associated
[ 1151.907071] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[ 1188.835291] wlan0: deauthenticating from  by local choice (Reason: 3=DEAUTH_LEAVING)
[ 1226.062720] wlan0: authenticate with 
[ 1227.243607] wlan0: send auth to  (try 1/3)
[ 1227.256704] wlan0: send auth to  (try 2/3)
[ 1227.269678] wlan0: send auth to  (try 3/3)
[ 1227.282518] wlan0: authentication with  timed out
[ 1232.179331] wlan0: authenticate with 
[ 1233.304162] wlan0: send auth to  (try 1/3)
[ 1233.308870] wlan0: authenticated
[ 1233.319511] wlan0: associate with  (try 1/3)
[ 1233.395893] wlan0: RX AssocResp from  (capab=0x1411 status=0 aid=2)
[ 1233.404445] wlan0: associated
[ 1233.404476] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[ 1233.416644] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[ 1256.885256] wlan0: deauthenticating from  by local choice (Reason: 3=DEAUTH_LEAVING)
[ 1340.800422] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
```

</details>

iperf3 cannot test connection keep dead and disconnected.

<details>

<summary>iperf3</summary>

```
```

</details>
