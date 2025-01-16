# RTL8821CU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="./image/8821cu/rtl8821cu_arm_a53_usb.JPG" height="400"/>|<img src="./image/8821cu/rtl8821cu_usb_pcba.JPG" height="400"/>|

```
Architecture:        armv7l
Byte Order:          Little Endian
CPU(s):              2
On-line CPU(s) list: 0,1
Thread(s) per core:  1
Core(s) per socket:  2
Socket(s):           1
Vendor ID:           ARM
Model:               0
Model name:          Cortex-A9
Stepping:            r3p0
BogoMIPS:            666.66
Flags:               half thumb fastmult vfp edsp neon vfpv3 tls vfpd32
```

### USB Tree

```
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Mass Storage, Driver=usb-storage, 480M
```

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8821cu             16384  0
rtw_8821c              90112  1 rtw_8821cu
rtw_usb                24576  1 rtw_8821cu
rtw_core              172032  2 rtw_usb,rtw_8821c

[   27.970244] usb 1-1.1: new high-speed USB device number 3 using xhci-hcd
[   28.094486] usb 1-1.1: New USB device found, idVendor=0bda, idProduct=1a2b, bcdDevice= 2.00
[   28.094492] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=0
[   28.094497] usb 1-1.1: Product: DISK
[   28.094501] usb 1-1.1: Manufacturer: Realtek
[   28.095193] usb-storage 1-1.1:1.0: USB Mass Storage device detected
[   28.097311] scsi host0: usb-storage 1-1.1:1.0
[   28.341189] usb 1-1.1: USB disconnect, device number 3
[   28.590242] usb 1-1.1: new high-speed USB device number 4 using xhci-hcd
[   28.714391] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x3 has wMaxPacketSize 0, skipping
[   28.714398] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x83 has wMaxPacketSize 0, skipping
[   28.714564] usb 1-1.1: New USB device found, idVendor=0bda, idProduct=c820, bcdDevice= 2.00
[   28.714570] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[   28.714574] usb 1-1.1: Product: 802.11ac NIC
[   28.714578] usb 1-1.1: Manufacturer: Realtek
[   28.714583] usb 1-1.1: SerialNumber: 123456
[   28.828650] Bluetooth: hci0: RTL: examining hci_ver=08 hci_rev=000c lmp_ver=08 lmp_subver=8821
[   28.829618] Bluetooth: hci0: RTL: rom_version status=0 version=1
[   28.829623] Bluetooth: hci0: RTL: loading rtl_bt/rtl8821c_fw.bin
[   28.834554] Bluetooth: hci0: RTL: loading rtl_bt/rtl8821c_config.bin
[   28.835339] Bluetooth: hci0: RTL: cfg_sz 10, total sz 34926
[   29.298622] Bluetooth: hci0: RTL: fw version 0x75b8f098
[   42.886823] rtw_core: loading out-of-tree module taints kernel.
[   50.670286] rtw_8821cu 1-1.1:1.2: Firmware version 24.11.0, H2C version 12
[   51.027153] usbcore: registered new interface driver rtw_8821cu

```

There is a possible issue could happen on ARM and other platform.

If the USB is loaded as a disk. 

Modify the rules, and the ID might be different (please replace with necessary)

>vi /lib/udev/rules.d/40-usb_modeswitch.rules

```
# Realtek 8211CU Wifi AC USB
ATTR{idVendor}=="0bda", ATTR{idProduct}=="1a2b", RUN+="/usr/sbin/usb_modeswitch -K -v 0bda -p 1a2b"
```

### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.26  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 24  bytes 3794 (3.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 21  bytes 2584 (2.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     4.85 ms   (jitter: 1.72ms, low: 2.99ms, high: 8.06ms)
    Download:    34.46 Mbps (data used: 17.3 MB)
                203.88 ms   (jitter: 57.93ms, low: 11.17ms, high: 447.52ms)
      Upload:    19.32 Mbps (data used: 33.6 MB)
                346.56 ms   (jitter: 73.56ms, low: 21.69ms, high: 1902.33ms)
```
### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=4.59 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=4.27 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.29 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=3.68 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=3.05 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=6.68 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=9.19 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=3.30 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=6.16 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=3.31 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=8.17 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=3.44 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=3.05 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=8.67 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=4.79 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=6.43 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=3.06 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=8.67 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=3.67 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=6.03 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 3.056/5.180/9.190/2.098 ms
```

#### Self-Ping 

```
PING 192.168.1.26 (192.168.1.26) 10000(10028) bytes of data.
10008 bytes from 192.168.1.26: icmp_seq=1 ttl=64 time=0.102 ms
10008 bytes from 192.168.1.26: icmp_seq=2 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.26: icmp_seq=3 ttl=64 time=0.070 ms
10008 bytes from 192.168.1.26: icmp_seq=4 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.26: icmp_seq=5 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.26: icmp_seq=6 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.26: icmp_seq=7 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.26: icmp_seq=8 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.26: icmp_seq=9 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.26: icmp_seq=10 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.26: icmp_seq=11 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.26: icmp_seq=12 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.26: icmp_seq=13 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.26: icmp_seq=14 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.26: icmp_seq=15 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.26: icmp_seq=16 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.26: icmp_seq=17 ttl=64 time=0.058 ms
10008 bytes from 192.168.1.26: icmp_seq=18 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.26: icmp_seq=19 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.26: icmp_seq=20 ttl=64 time=0.060 ms

--- 192.168.1.26 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19457ms
rtt min/avg/max/mdev = 0.058/0.062/0.102/0.013 ms
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
        max # scan plans: 1
        max scan plan interval: -1
        max scan plan iterations: 0
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
                 * set_tx_bitrate_mask
                 * frame
                 * frame_wait_cancel
                 * set_wiphy_netns
                 * set_channel
                 * set_wds_peer
                 * tdls_mgmt
                 * tdls_oper
                 * probe_client
                 * set_noack_map
                 * register_beacons
                 * start_p2p_device
                 * set_mcast_rate
                 * testmode
                 * connect
                 * disconnect
                 * set_qos_map
                 * set_multicast_to_unicast
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
                 * managed: 0x40 0xd0
                 * AP: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * AP/VLAN: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * mesh point: 0xb0 0xc0 0xd0
                 * P2P-client: 0x40 0xd0
                 * P2P-GO: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * P2P-device: 0x40 0xd0
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
```

</details>

### iwconfig

```
wlan0     IEEE 802.11  ESSID:""
          Mode:Managed  Frequency:2.412 GHz  Access Point: F8:6F:B0:0E:AE:E5
          Bit Rate=40.5 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=50/70  Signal level=-60 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:39   Missed beacon:0
```
### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 62867
[  5] local 192.168.1.26 port 5201 connected to 192.168.1.3 port 62868
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.59 MBytes  21.7 Mbits/sec    0    134 KBytes
[  5]   1.00-2.00   sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]   2.00-3.00   sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes
[  5]   3.00-4.00   sec  1.90 MBytes  15.9 Mbits/sec    0    134 KBytes
[  5]   4.00-5.00   sec  1.23 MBytes  10.3 Mbits/sec    0    134 KBytes
[  5]   5.00-6.00   sec  1.96 MBytes  16.4 Mbits/sec    0    134 KBytes
[  5]   6.00-7.00   sec  1.59 MBytes  13.4 Mbits/sec    0    134 KBytes
[  5]   7.00-8.00   sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]   8.00-9.00   sec  2.27 MBytes  19.0 Mbits/sec    0    134 KBytes
[  5]   9.00-10.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
[  5]  10.00-11.00  sec  2.33 MBytes  19.5 Mbits/sec    0    134 KBytes
[  5]  11.00-12.00  sec  2.76 MBytes  23.1 Mbits/sec    0    134 KBytes
[  5]  12.00-13.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]  13.00-14.00  sec  2.33 MBytes  19.5 Mbits/sec    0    134 KBytes
[  5]  14.00-15.00  sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]  15.00-16.00  sec  2.63 MBytes  22.1 Mbits/sec    0    134 KBytes
[  5]  16.00-17.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]  17.00-18.00  sec  2.82 MBytes  23.6 Mbits/sec    0    134 KBytes
[  5]  18.00-19.00  sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes
[  5]  19.00-20.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]  20.00-21.00  sec  2.76 MBytes  23.1 Mbits/sec    0    134 KBytes
[  5]  21.00-22.00  sec  2.21 MBytes  18.5 Mbits/sec    0    134 KBytes
[  5]  22.00-23.00  sec  1.90 MBytes  15.9 Mbits/sec    0    134 KBytes
[  5]  23.00-24.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]  24.00-25.00  sec  2.82 MBytes  23.6 Mbits/sec    0    134 KBytes
[  5]  25.00-26.00  sec  2.70 MBytes  22.6 Mbits/sec    0    134 KBytes
[  5]  26.00-27.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]  27.00-28.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes
[  5]  28.00-29.00  sec  2.88 MBytes  24.2 Mbits/sec    0    134 KBytes
[  5]  29.00-30.00  sec  2.27 MBytes  19.0 Mbits/sec    0    134 KBytes
[  5]  30.00-31.00  sec  2.82 MBytes  23.6 Mbits/sec    0    134 KBytes
[  5]  31.00-32.00  sec  3.12 MBytes  26.2 Mbits/sec    0    134 KBytes
[  5]  32.00-33.00  sec  2.82 MBytes  23.6 Mbits/sec    0    134 KBytes
[  5]  33.00-34.00  sec  2.45 MBytes  20.6 Mbits/sec    0    134 KBytes
[  5]  34.00-35.00  sec  2.45 MBytes  20.6 Mbits/sec    0    134 KBytes
[  5]  35.00-36.00  sec  1.29 MBytes  10.8 Mbits/sec    1    134 KBytes
[  5]  36.00-37.00  sec  1.90 MBytes  15.9 Mbits/sec    0    134 KBytes
[  5]  37.00-38.00  sec  1.35 MBytes  11.3 Mbits/sec    1    134 KBytes
[  5]  38.00-39.00  sec  2.45 MBytes  20.6 Mbits/sec    0    134 KBytes
[  5]  39.00-40.00  sec  2.27 MBytes  19.0 Mbits/sec    0    134 KBytes
[  5]  40.00-41.00  sec  1.90 MBytes  15.9 Mbits/sec    0    134 KBytes
[  5]  41.00-42.00  sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes
[  5]  42.00-43.00  sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]  43.00-44.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
[  5]  44.00-45.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
[  5]  45.00-46.00  sec  2.21 MBytes  18.5 Mbits/sec    0    134 KBytes
[  5]  46.00-47.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
[  5]  47.00-48.00  sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]  48.00-49.00  sec  1004 KBytes  8.22 Mbits/sec    0    134 KBytes
[  5]  49.00-50.00  sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]  50.00-51.00  sec  2.27 MBytes  19.0 Mbits/sec    0    134 KBytes
[  5]  51.00-52.00  sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]  52.00-53.00  sec  1.90 MBytes  15.9 Mbits/sec    0    134 KBytes
[  5]  53.00-54.00  sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes
[  5]  54.00-55.00  sec  1.23 MBytes  10.3 Mbits/sec    0    134 KBytes
[  5]  55.00-56.00  sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes
[  5]  56.00-57.00  sec  1.23 MBytes  10.3 Mbits/sec    0    134 KBytes
[  5]  57.00-58.00  sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes
[  5]  58.00-59.00  sec  1.29 MBytes  10.8 Mbits/sec    0    134 KBytes
[  5]  59.00-60.00  sec  1.53 MBytes  12.9 Mbits/sec    0    134 KBytes
[  5]  60.00-61.00  sec  2.14 MBytes  18.0 Mbits/sec    0    134 KBytes
[  5]  61.00-62.00  sec  2.82 MBytes  23.6 Mbits/sec    0    134 KBytes
[  5]  62.00-63.00  sec  2.57 MBytes  21.6 Mbits/sec    0    134 KBytes
[  5]  63.00-64.00  sec  1.59 MBytes  13.4 Mbits/sec    0    134 KBytes
[  5]  64.00-65.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
[  5]  65.00-66.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
[  5]  65.00-66.00  sec  1.53 MBytes  12.8 Mbits/sec    0    134 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-66.00  sec   139 MBytes  17.7 Mbits/sec    2             sender
[  5]   0.00-66.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
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
<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 51257
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 51258
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  3.90 MBytes  32.7 Mbits/sec    0   67.0 KBytes
[  5]   1.00-2.00   sec  3.80 MBytes  31.9 Mbits/sec    0   78.4 KBytes
[  5]   2.00-3.00   sec  3.61 MBytes  30.3 Mbits/sec    0    184 KBytes
[  5]   3.00-4.00   sec  2.57 MBytes  21.6 Mbits/sec    0    210 KBytes
[  5]   4.00-5.00   sec  1.84 MBytes  15.4 Mbits/sec    0    218 KBytes
[  5]   5.00-6.00   sec  2.27 MBytes  19.0 Mbits/sec    0    218 KBytes
[  5]   6.00-7.00   sec  2.94 MBytes  24.7 Mbits/sec    0    230 KBytes
[  5]   7.00-8.00   sec  2.02 MBytes  17.0 Mbits/sec    0    230 KBytes
[  5]   8.00-9.00   sec  3.00 MBytes  25.2 Mbits/sec    0    312 KBytes
[  5]   9.00-10.00  sec  3.49 MBytes  29.3 Mbits/sec    0    443 KBytes
[  5]  10.00-11.00  sec  1.78 MBytes  14.9 Mbits/sec    0    443 KBytes
[  5]  11.00-12.00  sec  2.70 MBytes  22.6 Mbits/sec    0    443 KBytes
[  5]  12.00-13.00  sec  3.74 MBytes  31.4 Mbits/sec    0    663 KBytes
[  5]  13.00-14.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  14.00-15.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  15.00-16.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  16.00-17.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  17.00-18.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  18.00-19.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  19.00-20.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  20.00-21.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  21.00-22.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  22.00-23.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  23.00-24.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  24.00-25.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  25.00-26.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  26.00-27.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  27.00-28.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  28.00-29.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  29.00-30.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  30.00-31.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  31.00-32.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  32.00-33.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  33.00-34.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  34.00-35.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  35.00-36.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  36.00-37.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  37.00-38.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  38.00-39.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  39.00-40.00  sec  1.25 MBytes  10.5 Mbits/sec    0    663 KBytes
[  5]  40.00-41.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  41.00-42.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  42.00-43.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  43.00-44.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  44.00-45.00  sec  3.75 MBytes  31.5 Mbits/sec    0    663 KBytes
[  5]  45.00-46.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
[  5]  45.00-46.00  sec  2.50 MBytes  21.0 Mbits/sec    0    663 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-46.00  sec   143 MBytes  26.0 Mbits/sec    0             sender
[  5]   0.00-46.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
