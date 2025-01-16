# RTL8812AU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/8cf97d5b-a307-4d4e-8770-58cee0fd1843" height="400"/>|<img src="https://github.com/user-attachments/assets/7473222c-3969-4c74-9c19-629dbdb79321" height="400"/>|

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
    |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=rtw_8812au, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 003: ID 0bda:8812 Realtek Semiconductor Corp. RTL8812AU 802.11a/b/g/n/ac 2T2R DB WLAN Adapter
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.10
  bDeviceClass            0
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0x8812 RTL8812AU 802.11a/b/g/n/ac 2T2R DB WLAN Adapter
  bcdDevice            0.00
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength       0x0035
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
      bNumEndpoints           5
      bInterfaceClass       255 Vendor Specific Class
      bInterfaceSubClass    255 Vendor Specific Subclass
      bInterfaceProtocol    255 Vendor Specific Protocol
      iInterface              0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x81  EP 1 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x02  EP 2 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x04  EP 4 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x85  EP 5 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               1
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[   52.441280] rtw_core: loading out-of-tree module taints kernel.
[   62.766890] rtw_8812au 1-1:1.0: Firmware version 52.14.0, H2C version 0
[   63.203393] usbcore: registered new interface driver rtw_8812au
[   63.248331] usb 1-1: USB disconnect, device number 2
[   63.688187] usb 1-1: new high-speed USB device number 3 using dwc2
[   63.896676] usb 1-1: New USB device found, idVendor=0bda, idProduct=8812, bcdDevice= 0.00
[   63.896699] usb 1-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[   63.896709] usb 1-1: Product: 802.11n NIC
[   63.896717] usb 1-1: Manufacturer: Realtek
[   63.896725] usb 1-1: SerialNumber: 123456
[   63.897631] rtw_8812au 1-1:1.0: Firmware version 52.14.0, H2C version 0

Module                  Size  Used by
rtw_8812au             16384  0
rtw_8812a              49152  1 rtw_8812au
rtw_88xxa              36864  1 rtw_8812a
rtw_usb                24576  1 rtw_8812au
rtw_core              217088  3 rtw_88xxa,rtw_usb,rtw_8812a
```

### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.25  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 21  bytes 2609 (2.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 27  bytes 4688 (4.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     3.42 ms   (jitter: 0.39ms, low: 3.15ms, high: 4.68ms)
    Download:    58.46 Mbps (data used: 93.4 MB)
                183.95 ms   (jitter: 56.55ms, low: 53.70ms, high: 489.62ms)
      Upload:    37.81 Mbps (data used: 32.6 MB)
                 54.78 ms   (jitter: 10.94ms, low: 10.78ms, high: 144.56ms)
```
### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=72.3 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=198 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=17.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=142 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=61.8 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=188 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=111 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=133 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=153 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=177 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=202 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=120 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=37.2 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=167 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=190 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=219 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=30.2 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=163 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=72.4 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=198 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 17.188/132.590/218.917/62.274 ms
```

#### Self-Ping 

```
PING 192.168.1.25 (192.168.1.25) 10000(10028) bytes of data.
10008 bytes from 192.168.1.25: icmp_seq=1 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.25: icmp_seq=2 ttl=64 time=0.133 ms
10008 bytes from 192.168.1.25: icmp_seq=3 ttl=64 time=0.094 ms
10008 bytes from 192.168.1.25: icmp_seq=4 ttl=64 time=0.079 ms
10008 bytes from 192.168.1.25: icmp_seq=5 ttl=64 time=0.092 ms
10008 bytes from 192.168.1.25: icmp_seq=6 ttl=64 time=0.087 ms
10008 bytes from 192.168.1.25: icmp_seq=7 ttl=64 time=0.099 ms
10008 bytes from 192.168.1.25: icmp_seq=8 ttl=64 time=0.077 ms
10008 bytes from 192.168.1.25: icmp_seq=9 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.25: icmp_seq=10 ttl=64 time=0.079 ms
10008 bytes from 192.168.1.25: icmp_seq=11 ttl=64 time=0.083 ms
10008 bytes from 192.168.1.25: icmp_seq=12 ttl=64 time=0.076 ms
10008 bytes from 192.168.1.25: icmp_seq=13 ttl=64 time=0.111 ms
10008 bytes from 192.168.1.25: icmp_seq=14 ttl=64 time=0.086 ms
10008 bytes from 192.168.1.25: icmp_seq=15 ttl=64 time=0.081 ms
10008 bytes from 192.168.1.25: icmp_seq=16 ttl=64 time=0.084 ms
10008 bytes from 192.168.1.25: icmp_seq=17 ttl=64 time=0.092 ms
10008 bytes from 192.168.1.25: icmp_seq=18 ttl=64 time=0.075 ms
10008 bytes from 192.168.1.25: icmp_seq=19 ttl=64 time=0.125 ms
10008 bytes from 192.168.1.25: icmp_seq=20 ttl=64 time=0.084 ms

--- 192.168.1.25 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19450ms
rtt min/avg/max/mdev = 0.075/0.093/0.133/0.017 ms
```

### iw list

<details>

<summary>iw list</summary>

```
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
        Available Antennas: TX 0x3 RX 0x3
        Configured Antennas: TX 0x3 RX 0x3
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
                HT Max RX data rate: 300 Mbps
                HT TX/RX MCS rate indexes supported: 0-15, 32
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
                Minimum RX AMPDU time spacing: 16 usec (0x07)
                HT Max RX data rate: 300 Mbps
                HT TX/RX MCS rate indexes supported: 0-15, 32
                VHT Capabilities (0x03d071a2):
                        Max MPDU length: 11454
                        Supported Channel Width: neither 160 nor 80+80
                        short GI (80 MHz)
                        TX STBC
                        SU Beamformee
                        MU Beamformee
                        +HTC-VHT
                VHT RX MCS set:
                        1 streams: MCS 0-9
                        2 streams: MCS 0-9
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT RX highest supported: 780 Mbps
                VHT TX MCS set:
                        1 streams: MCS 0-9
                        2 streams: MCS 0-9
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT TX highest supported: 780 Mbps
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

```
wlan0     IEEE 802.11  ESSID:""
          Mode:Managed  Frequency:2.412 GHz  Access Point: F8:6F:B0:0E:AE:E5
          Bit Rate=40.5 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=54/70  Signal level=-56 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:24   Missed beacon:0
```
### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.32, port 60894
[  5] local 192.168.1.25 port 5201 connected to 192.168.1.32 port 60896
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  2.22 MBytes  18.6 Mbits/sec    0    133 KBytes
[  5]   1.00-2.00   sec  1.84 MBytes  15.4 Mbits/sec    0    133 KBytes
[  5]   2.00-3.00   sec  2.14 MBytes  18.0 Mbits/sec    0    133 KBytes
[  5]   3.00-4.00   sec  2.14 MBytes  18.0 Mbits/sec   26   94.1 KBytes
[  5]   4.00-5.00   sec  1.84 MBytes  15.4 Mbits/sec    2   79.8 KBytes
[  5]   5.00-6.00   sec  2.14 MBytes  18.0 Mbits/sec    0   99.8 KBytes
[  5]   6.00-7.00   sec  3.98 MBytes  33.4 Mbits/sec    0    127 KBytes
[  5]   7.00-8.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   8.00-9.00   sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]   9.00-10.00  sec  2.45 MBytes  20.6 Mbits/sec    0    130 KBytes
[  5]  10.00-11.00  sec  2.76 MBytes  23.1 Mbits/sec    0    130 KBytes
[  5]  11.00-12.00  sec  2.45 MBytes  20.6 Mbits/sec    0    130 KBytes
[  5]  12.00-13.00  sec  2.76 MBytes  23.1 Mbits/sec    0    130 KBytes
[  5]  13.00-14.00  sec  2.45 MBytes  20.6 Mbits/sec    0    130 KBytes
[  5]  14.00-15.00  sec  2.94 MBytes  24.7 Mbits/sec    0    197 KBytes
[  5]  15.00-16.00  sec  2.57 MBytes  21.6 Mbits/sec    0    197 KBytes
[  5]  16.00-17.00  sec  3.00 MBytes  25.2 Mbits/sec    0    197 KBytes
[  5]  17.00-18.00  sec  2.57 MBytes  21.6 Mbits/sec    0    197 KBytes
[  5]  18.00-19.00  sec  2.57 MBytes  21.6 Mbits/sec    0    197 KBytes
[  5]  19.00-20.00  sec  2.57 MBytes  21.6 Mbits/sec    0    197 KBytes
[  5]  20.00-21.00  sec  2.57 MBytes  21.6 Mbits/sec    0    197 KBytes
[  5]  21.00-22.00  sec  2.14 MBytes  18.0 Mbits/sec    0    197 KBytes
[  5]  22.00-23.00  sec  3.00 MBytes  25.2 Mbits/sec    0    197 KBytes
[  5]  23.00-24.00  sec  2.14 MBytes  18.0 Mbits/sec    0    197 KBytes
[  5]  24.00-25.00  sec  2.14 MBytes  18.0 Mbits/sec    0    197 KBytes
[  5]  24.00-25.00  sec  2.14 MBytes  18.0 Mbits/sec    0    197 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-25.00  sec  65.3 MBytes  21.9 Mbits/sec   28             sender
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
Using interface wlan0 with hwaddr  and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

There are unconditional warning messages.

<details>

<summary>dmesg</summary>

```
[  467.423318] rtw_8812au 1-1:1.0: error beacon valid
[  467.423516] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  475.810486] rtw_8812au 1-1:1.0: error beacon valid
[  475.810691] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  475.914084] rtw_8812au 1-1:1.0: error beacon valid
[  475.914270] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  475.914280] rtw_8812au 1-1:1.0: failed to download beacon
[  477.353071] rtw_8812au 1-1:1.0: error beacon valid
[  477.353280] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  477.353290] rtw_8812au 1-1:1.0: failed to download beacon
[  490.454336] rtw_8812au 1-1:1.0: error beacon valid
[  490.454543] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  490.454554] rtw_8812au 1-1:1.0: failed to download beacon
[  498.140317] rtw_8812au 1-1:1.0: error beacon valid
[  498.140527] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  501.104453] rtw_8812au 1-1:1.0: error beacon valid
[  501.104635] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  501.104646] rtw_8812au 1-1:1.0: failed to download beacon
[  501.211908] rtw_8812au 1-1:1.0: error beacon valid
[  501.212096] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  506.946621] rtw_8812au 1-1:1.0: error beacon valid
[  506.946811] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  506.946822] rtw_8812au 1-1:1.0: failed to download beacon
[  512.471415] rtw_8812au 1-1:1.0: error beacon valid
[  512.471621] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  515.846264] rtw_8812au 1-1:1.0: error beacon valid
[  515.846456] rtw_8812au 1-1:1.0: failed to download drv rsvd page
```

</details>

No disconnection, but speed drop and temporary stuck.

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.193, port 59548
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.193 port 59549
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  2.53 MBytes  21.2 Mbits/sec   70   75.6 KBytes
[  467.423318] rtw_8812au 1-1:1.0: error beacon valid
[  467.423516] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  5]   1.00-2.00   sec  1.72 MBytes  14.4 Mbits/sec    0    110 KBytes
[  5]   2.00-3.00   sec  1.96 MBytes  16.4 Mbits/sec    0    110 KBytes
[  5]   3.00-4.00   sec  1.72 MBytes  14.4 Mbits/sec   20   17.1 KBytes
[  5]   4.00-5.00   sec  1.47 MBytes  12.3 Mbits/sec   41   91.2 KBytes
[  5]   5.00-6.00   sec  1.72 MBytes  14.4 Mbits/sec   61   72.7 KBytes
[  5]   6.00-7.00   sec  1.47 MBytes  12.3 Mbits/sec    0   88.4 KBytes
[  5]   7.00-8.00   sec  1.53 MBytes  12.8 Mbits/sec    0    101 KBytes
[  5]   8.00-9.00   sec  1.47 MBytes  12.3 Mbits/sec   61    107 KBytes
[  475.810486] rtw_8812au 1-1:1.0: error beacon valid
[  475.810691] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  475.914084] rtw_8812au 1-1:1.0: error beacon valid
[  475.914270] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  475.914280] rtw_8812au 1-1:1.0: failed to download beacon
[  5]   9.00-10.00  sec  1.47 MBytes  12.3 Mbits/sec   62    107 KBytes
[  5]  10.00-11.00  sec  1.47 MBytes  12.3 Mbits/sec   71    107 KBytes
[  477.353071] rtw_8812au 1-1:1.0: error beacon valid
[  477.353280] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  477.353290] rtw_8812au 1-1:1.0: failed to download beacon
[  5]  11.00-12.00  sec  1.23 MBytes  10.3 Mbits/sec   67   79.8 KBytes
[  5]  12.00-13.00  sec  1.72 MBytes  14.4 Mbits/sec    0   94.1 KBytes
[  5]  13.00-14.00  sec  1.47 MBytes  12.3 Mbits/sec   65   72.7 KBytes
[  5]  14.00-15.00  sec  1.72 MBytes  14.4 Mbits/sec    0   72.7 KBytes
[  5]  15.00-16.00  sec  1.47 MBytes  12.3 Mbits/sec    0   84.1 KBytes
[  5]  16.00-17.00  sec  1.47 MBytes  12.3 Mbits/sec    0   97.0 KBytes
[  5]  17.00-18.00  sec  1.53 MBytes  12.8 Mbits/sec   66   72.7 KBytes
[  5]  18.00-19.00  sec  1.47 MBytes  12.3 Mbits/sec    0   72.7 KBytes
[  5]  19.00-20.00  sec  1.47 MBytes  12.3 Mbits/sec   28   45.6 KBytes
[  5]  20.00-21.00  sec  1.47 MBytes  12.3 Mbits/sec   34   14.3 KBytes
[  5]  21.00-22.00  sec  1.23 MBytes  10.3 Mbits/sec   30   31.4 KBytes
[  5]  22.00-23.00  sec  1.47 MBytes  12.3 Mbits/sec   33   32.8 KBytes
[  5]  23.00-24.00  sec  1.47 MBytes  12.3 Mbits/sec    0   52.8 KBytes
[  490.454336] rtw_8812au 1-1:1.0: error beacon valid
[  490.454543] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  490.454554] rtw_8812au 1-1:1.0: failed to download beacon
[  5]  24.00-25.00  sec  1.23 MBytes  10.3 Mbits/sec   42   45.6 KBytes
[  5]  25.00-26.00  sec  1.47 MBytes  12.3 Mbits/sec    1   58.5 KBytes
[  5]  26.00-27.00  sec  1.23 MBytes  10.3 Mbits/sec    0   74.1 KBytes
[  5]  27.00-28.00  sec  1.23 MBytes  10.3 Mbits/sec   49   67.0 KBytes
[  5]  28.00-29.00  sec  1.47 MBytes  12.3 Mbits/sec    0   81.3 KBytes
[  5]  29.00-30.00  sec  1.47 MBytes  12.3 Mbits/sec    0   95.5 KBytes
[  5]  30.00-31.00  sec  1.47 MBytes  12.3 Mbits/sec   66    104 KBytes
[  498.140317] rtw_8812au 1-1:1.0: error beacon valid
[  498.140527] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  5]  31.00-32.00  sec  1.72 MBytes  14.4 Mbits/sec    0    104 KBytes
[  5]  32.00-33.00  sec  1.23 MBytes  10.3 Mbits/sec  121   79.8 KBytes
[  5]  33.00-34.00  sec  1.96 MBytes  16.4 Mbits/sec    0   97.0 KBytes
[  501.104453] rtw_8812au 1-1:1.0: error beacon valid
[  501.104635] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  501.104646] rtw_8812au 1-1:1.0: failed to download beacon
[  5]  34.00-35.00  sec  1.23 MBytes  10.3 Mbits/sec   62   49.9 KBytes
[  501.211908] rtw_8812au 1-1:1.0: error beacon valid
[  501.212096] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  5]  35.00-36.00  sec  1.47 MBytes  12.3 Mbits/sec   48   64.2 KBytes
[  5]  36.00-37.00  sec  1.23 MBytes  10.3 Mbits/sec    0   78.4 KBytes
[  5]  37.00-38.00  sec  1.72 MBytes  14.4 Mbits/sec    0   94.1 KBytes
[  5]  38.00-39.00  sec  1.47 MBytes  12.3 Mbits/sec   58   74.1 KBytes
[  5]  39.00-40.00  sec  1.72 MBytes  14.4 Mbits/sec    0   91.2 KBytes
[  506.946621] rtw_8812au 1-1:1.0: error beacon valid
[  506.946811] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  506.946822] rtw_8812au 1-1:1.0: failed to download beacon
[  5]  40.00-41.00  sec  1.47 MBytes  12.3 Mbits/sec    0    103 KBytes
[  5]  41.00-42.00  sec  1.96 MBytes  16.4 Mbits/sec    0    115 KBytes
[  5]  42.00-43.00  sec  1.47 MBytes  12.3 Mbits/sec   65   62.7 KBytes
[  5]  43.00-44.00  sec  1.90 MBytes  15.9 Mbits/sec    0   78.4 KBytes
[  5]  44.00-45.00  sec  1.29 MBytes  10.8 Mbits/sec    0   92.7 KBytes
[  5]  45.00-46.00  sec  1.72 MBytes  14.4 Mbits/sec   66    103 KBytes
[  512.471415] rtw_8812au 1-1:1.0: error beacon valid
[  512.471621] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  5]  46.00-47.00  sec  1.47 MBytes  12.3 Mbits/sec    0    103 KBytes
[  5]  47.00-48.00  sec  1.78 MBytes  14.9 Mbits/sec    9   7.13 KBytes
[  5]  48.00-49.00  sec  1.29 MBytes  10.8 Mbits/sec   49   84.1 KBytes
[  515.846264] rtw_8812au 1-1:1.0: error beacon valid
[  515.846456] rtw_8812au 1-1:1.0: failed to download drv rsvd page
[  5]  49.00-50.00  sec  1.59 MBytes  13.4 Mbits/sec    0   97.0 KBytes
[  5]  50.00-51.00  sec  1.29 MBytes  10.8 Mbits/sec    0    107 KBytes
[  5]  51.00-52.00  sec  1.84 MBytes  15.4 Mbits/sec   65    115 KBytes
[  5]  52.00-53.00  sec  1.65 MBytes  13.9 Mbits/sec   68   79.8 KBytes
[  5]  53.00-54.00  sec  2.02 MBytes  17.0 Mbits/sec    0   81.3 KBytes
[  5]  54.00-55.00  sec  1.90 MBytes  15.9 Mbits/sec    0   98.4 KBytes
[  5]  55.00-56.00  sec  1.90 MBytes  15.9 Mbits/sec   67    108 KBytes
[  5]  56.00-57.00  sec  1.53 MBytes  12.8 Mbits/sec   68   75.6 KBytes
[  5]  57.00-58.00  sec  1.47 MBytes  12.3 Mbits/sec    0   77.0 KBytes
[  5]  58.00-59.00  sec  2.08 MBytes  17.5 Mbits/sec    0   94.1 KBytes
[  5]  59.00-60.00  sec  1.78 MBytes  14.9 Mbits/sec    0    108 KBytes
[  5]  60.00-61.00  sec  1.59 MBytes  13.4 Mbits/sec    0   92.7 KBytes
[  5]  61.00-62.00  sec  1.47 MBytes  12.3 Mbits/sec    0    106 KBytes
[  5]  61.00-62.00  sec  1.47 MBytes  12.3 Mbits/sec    0    106 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-62.00  sec  97.9 MBytes  13.2 Mbits/sec  1613             sender
```

</details>
