# RTL8723DU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="./image/8723du/rtl8723du_arm_a9.png" height="400"/>|<img src="./image/8723du/rtl8723du_usb_pcba.png" height="400"/>|

```
uname -r
5.4.0

lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.5 LTS
Release:        18.04
Codename:       bionic

lscpu
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
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/2p, 480M
        |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=rtw_8723du, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 003: ID 0bda:d723 Realtek Semiconductor Corp.
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2 ?
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xd723
  bcdDevice            2.00
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength          236
    bNumInterfaces          3
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0xe0
      Self Powered
      Remote Wakeup
    MaxPower              500mA
    Interface Association:
      bLength                 8
      bDescriptorType        11
      bFirstInterface         0
      bInterfaceCount         2
      bFunctionClass        224 Wireless
      bFunctionSubClass       1 Radio Frequency
      bFunctionProtocol       1 Bluetooth
      iFunction               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           3
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x81  EP 1 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0010  1x 16 bytes
        bInterval               4
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
        bEndpointAddress     0x82  EP 2 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       0
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0000  1x 0 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0000  1x 0 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       1
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0009  1x 9 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0009  1x 9 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       2
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0011  1x 17 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0011  1x 17 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       3
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0019  1x 25 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0019  1x 25 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       4
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0021  1x 33 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0021  1x 33 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       5
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0031  1x 49 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0031  1x 49 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        2
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
[   33.614209] usb 1-1.1: new high-speed USB device number 3 using ci_hdrc
[   33.764709] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x3 has wMaxPacketSize 0, skipping
[   33.764727] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x83 has wMaxPacketSize 0, skipping
[   33.786696] Bluetooth: hci0: RTL: examining hci_ver=08 hci_rev=000d lmp_ver=08 lmp_subver=8723
[   33.787618] Bluetooth: hci0: RTL: rom_version status=0 version=2
[   33.787630] Bluetooth: hci0: RTL: loading rtl_bt/rtl8723d_fw.bin
[   34.317635] Bluetooth: hci0: RTL: loading rtl_bt/rtl8723d_config.bin
[   34.322528] Bluetooth: hci0: RTL: cfg_sz 10, total sz 33266
[   34.586501] Bluetooth: hci0: RTL: fw version 0x828a96f1
[   36.026880] rtw_core: loading out-of-tree module taints kernel.
[   36.425083] rtw_8723du 1-1.1:1.2: Firmware version 48.0.0, H2C version 0
[   37.552014] usbcore: registered new interface driver rtw_8723du

Module                  Size  Used by
rtw_8723du             16384  0
rtw_8723d              40960  1 rtw_8723du
rtw_8723x              20480  1 rtw_8723d
rtw_usb                24576  1 rtw_8723du
rtw_core              172032  3 rtw_usb,rtw_8723d,rtw_8723x
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.23  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 29500  bytes 27709681 (27.7 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 35250  bytes 40221711 (40.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     5.42 ms   (jitter: 3.25ms, low: 3.64ms, high: 8.14ms)
    Download:    18.05 Mbps (data used: 17.0 MB)
                 31.01 ms   (jitter: 23.35ms, low: 4.86ms, high: 322.71ms)
      Upload:    20.13 Mbps (data used: 35.4 MB)
                138.29 ms   (jitter: 52.87ms, low: 8.55ms, high: 806.61ms)
```
### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=7.14 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=4.04 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.77 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=4.32 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=10.2 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=9.54 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=4.06 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=5.06 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=4.07 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=4.21 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=9.70 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=7.04 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=4.07 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=10.2 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=11.9 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=5.92 ms

--- 8.8.8.8 ping statistics ---
16 packets transmitted, 16 received, 0% packet loss, time 15021ms
rtt min/avg/max/mdev = 3.776/6.584/11.958/2.750 ms
```

#### Self-Ping 

```
PING 192.168.1.23 (192.168.1.23) 10000(10028) bytes of data.
10008 bytes from 192.168.1.23: icmp_seq=1 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.23: icmp_seq=2 ttl=64 time=0.117 ms
10008 bytes from 192.168.1.23: icmp_seq=3 ttl=64 time=0.113 ms
10008 bytes from 192.168.1.23: icmp_seq=4 ttl=64 time=0.116 ms
10008 bytes from 192.168.1.23: icmp_seq=5 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.23: icmp_seq=6 ttl=64 time=0.104 ms
10008 bytes from 192.168.1.23: icmp_seq=7 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.23: icmp_seq=8 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.23: icmp_seq=9 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.23: icmp_seq=10 ttl=64 time=0.126 ms
10008 bytes from 192.168.1.23: icmp_seq=11 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.23: icmp_seq=12 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.23: icmp_seq=13 ttl=64 time=0.102 ms
10008 bytes from 192.168.1.23: icmp_seq=14 ttl=64 time=0.100 ms
10008 bytes from 192.168.1.23: icmp_seq=15 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.23: icmp_seq=16 ttl=64 time=0.129 ms
10008 bytes from 192.168.1.23: icmp_seq=17 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.23: icmp_seq=18 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.23: icmp_seq=19 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.23: icmp_seq=20 ttl=64 time=0.103 ms

--- 192.168.1.23 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19742ms
rtt min/avg/max/mdev = 0.100/0.111/0.142/0.016 ms
```
### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy0
        max # scan SSIDs: 4
        max scan IEs length: 2257 bytes
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
wlan0     IEEE 802.11  ESSID:off/any
          Mode:Managed  Access Point: Not-Associated   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
```
### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 59012
[  5] local 192.168.1.23 port 5201 connected to 192.168.1.3 port 59013
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  3.03 MBytes  25.4 Mbits/sec    0    200 KBytes
[  5]   1.00-2.00   sec  2.70 MBytes  22.6 Mbits/sec    0    255 KBytes
[  5]   2.00-3.00   sec  3.12 MBytes  26.2 Mbits/sec    0    258 KBytes
[  5]   3.00-4.00   sec  2.88 MBytes  24.2 Mbits/sec    0    258 KBytes
[  5]   4.00-5.00   sec  2.45 MBytes  20.6 Mbits/sec    0    258 KBytes
[  5]   5.00-6.00   sec  2.76 MBytes  23.0 Mbits/sec    0    258 KBytes
[  5]   6.00-7.00   sec  2.45 MBytes  20.7 Mbits/sec    0    258 KBytes
[  5]   7.00-8.00   sec  2.14 MBytes  18.0 Mbits/sec    0    258 KBytes
[  5]   8.00-9.00   sec  2.51 MBytes  21.1 Mbits/sec    0    258 KBytes
[  5]   9.00-10.00  sec  2.21 MBytes  18.5 Mbits/sec    0    258 KBytes
[  5]  10.00-11.00  sec  2.51 MBytes  21.1 Mbits/sec    0    258 KBytes
[  5]  11.00-12.00  sec  2.51 MBytes  21.1 Mbits/sec    0    258 KBytes
[  5]  12.00-13.00  sec  3.43 MBytes  28.8 Mbits/sec    0    258 KBytes
[  5]  13.00-14.00  sec  2.88 MBytes  24.2 Mbits/sec    0    258 KBytes
[  5]  14.00-15.00  sec  1.84 MBytes  15.4 Mbits/sec    0    258 KBytes
[  5]  15.00-16.00  sec  3.12 MBytes  26.2 Mbits/sec    0    258 KBytes
[  5]  16.00-17.00  sec  3.31 MBytes  27.7 Mbits/sec    0    258 KBytes
[  5]  17.00-18.00  sec  3.06 MBytes  25.7 Mbits/sec    0    258 KBytes
[  5]  18.00-19.00  sec  3.12 MBytes  26.2 Mbits/sec    0    258 KBytes
[  5]  19.00-20.00  sec  3.31 MBytes  27.8 Mbits/sec    0    258 KBytes
[  5]  20.00-21.01  sec  3.06 MBytes  25.4 Mbits/sec    0    258 KBytes
[  5]  21.01-22.00  sec  3.12 MBytes  26.5 Mbits/sec    0    258 KBytes
[  5]  22.00-23.00  sec  3.12 MBytes  26.2 Mbits/sec    0    258 KBytes
[  5]  23.00-24.00  sec  4.04 MBytes  34.0 Mbits/sec    0    258 KBytes
[  5]  24.00-25.00  sec  3.74 MBytes  31.3 Mbits/sec    0    258 KBytes
[  5]  25.00-26.00  sec  4.10 MBytes  34.4 Mbits/sec    0    258 KBytes
[  5]  26.00-27.00  sec  4.41 MBytes  37.0 Mbits/sec    0    258 KBytes
[  5]  27.00-28.00  sec  3.86 MBytes  32.4 Mbits/sec    0    258 KBytes
[  5]  28.00-29.00  sec  3.86 MBytes  32.4 Mbits/sec    0    258 KBytes
[  5]  29.00-30.00  sec  3.74 MBytes  31.3 Mbits/sec    0    258 KBytes
[  5]  30.00-31.00  sec  3.55 MBytes  29.8 Mbits/sec    0    258 KBytes
[  5]  31.00-32.00  sec  3.12 MBytes  26.2 Mbits/sec    0    258 KBytes
[  5]  32.00-33.00  sec  2.57 MBytes  21.6 Mbits/sec    0    258 KBytes
[  5]  33.00-34.00  sec  3.86 MBytes  32.4 Mbits/sec    0    258 KBytes
[  5]  34.00-35.00  sec  4.17 MBytes  34.9 Mbits/sec    0    258 KBytes
[  5]  35.00-36.00  sec  4.66 MBytes  39.0 Mbits/sec    0    258 KBytes
[  5]  36.00-37.00  sec  3.92 MBytes  32.9 Mbits/sec    0    258 KBytes
[  5]  37.00-38.00  sec  4.47 MBytes  37.5 Mbits/sec    0    258 KBytes
[  5]  38.00-39.00  sec  3.55 MBytes  29.7 Mbits/sec    0    258 KBytes
[  5]  39.00-40.00  sec  4.23 MBytes  35.5 Mbits/sec    0    258 KBytes
[  5]  40.00-41.00  sec  3.98 MBytes  33.4 Mbits/sec    0    258 KBytes
[  5]  41.00-42.00  sec  2.70 MBytes  22.6 Mbits/sec  120   68.4 KBytes
[  5]  42.00-43.00  sec  2.51 MBytes  21.1 Mbits/sec    0   91.2 KBytes
[  5]  43.00-44.00  sec  2.21 MBytes  18.5 Mbits/sec    2   81.3 KBytes
[  5]  44.00-45.00  sec  3.74 MBytes  31.4 Mbits/sec    0    108 KBytes
[  5]  45.00-46.00  sec  3.49 MBytes  29.3 Mbits/sec    0    133 KBytes
[  5]  46.00-47.00  sec  2.82 MBytes  23.6 Mbits/sec    0    145 KBytes
[  5]  47.00-48.00  sec  4.17 MBytes  34.9 Mbits/sec    0    163 KBytes
[  5]  48.00-49.00  sec  4.04 MBytes  33.9 Mbits/sec    0    180 KBytes
[  5]  49.00-50.00  sec  4.17 MBytes  34.9 Mbits/sec    0    192 KBytes
[  5]  50.00-51.00  sec  3.80 MBytes  31.9 Mbits/sec    0    202 KBytes
[  5]  51.00-52.00  sec  3.80 MBytes  31.9 Mbits/sec    0    211 KBytes
[  5]  52.00-53.00  sec  4.35 MBytes  36.5 Mbits/sec    0    222 KBytes
[  5]  53.00-54.00  sec  4.17 MBytes  35.0 Mbits/sec    0    277 KBytes
[  5]  54.00-55.00  sec  3.61 MBytes  30.3 Mbits/sec    0    356 KBytes
[  5]  55.00-56.00  sec  3.61 MBytes  30.3 Mbits/sec    0    356 KBytes
[  5]  56.00-57.00  sec  3.19 MBytes  26.7 Mbits/sec    0    356 KBytes
[  5]  57.00-58.00  sec  3.43 MBytes  28.8 Mbits/sec    0    543 KBytes
[  5]  58.00-59.00  sec  3.49 MBytes  29.2 Mbits/sec    0    543 KBytes
[  5]  59.00-60.00  sec  3.61 MBytes  30.4 Mbits/sec    0    543 KBytes
[  5]  60.00-61.00  sec  4.10 MBytes  34.4 Mbits/sec    0    543 KBytes
[  5]  61.00-62.00  sec  3.49 MBytes  29.2 Mbits/sec    0    543 KBytes
[  5]  62.00-63.00  sec  4.10 MBytes  34.5 Mbits/sec    0    543 KBytes
[  5]  63.00-64.00  sec  4.10 MBytes  34.4 Mbits/sec    0    543 KBytes
[  5]  64.00-65.00  sec  2.88 MBytes  24.1 Mbits/sec    0    543 KBytes
[  5]  65.00-66.00  sec  3.55 MBytes  29.8 Mbits/sec    0    543 KBytes
[  5]  66.00-67.00  sec  3.55 MBytes  29.8 Mbits/sec    0    543 KBytes
[  5]  67.00-68.00  sec  3.55 MBytes  29.8 Mbits/sec    0    543 KBytes
[  5]  68.00-69.00  sec  3.43 MBytes  28.8 Mbits/sec    0    543 KBytes
[  5]  69.00-70.00  sec  3.00 MBytes  25.2 Mbits/sec    0    543 KBytes
[  5]  70.00-71.00  sec  4.04 MBytes  33.8 Mbits/sec    0    543 KBytes
[  5]  71.00-72.00  sec  4.10 MBytes  34.6 Mbits/sec    0    543 KBytes
[  5]  72.00-73.01  sec  4.17 MBytes  34.7 Mbits/sec    0    543 KBytes
[  5]  73.01-74.00  sec  4.59 MBytes  38.8 Mbits/sec    0    543 KBytes
[  5]  74.00-75.00  sec  3.98 MBytes  33.4 Mbits/sec    0    543 KBytes
[  5]  75.00-76.00  sec  4.23 MBytes  35.4 Mbits/sec    0    543 KBytes
[  5]  76.00-77.00  sec  4.53 MBytes  38.1 Mbits/sec    0    543 KBytes
[  5]  77.00-78.00  sec  4.23 MBytes  35.5 Mbits/sec    0    543 KBytes
[  5]  78.00-79.00  sec  4.17 MBytes  34.9 Mbits/sec    0    543 KBytes
[  5]  79.00-80.00  sec  3.37 MBytes  28.3 Mbits/sec    0    543 KBytes
[  5]  80.00-81.00  sec  4.59 MBytes  38.5 Mbits/sec    0    543 KBytes
[  5]  81.00-82.00  sec  3.61 MBytes  30.3 Mbits/sec    0    543 KBytes
[  5]  82.00-83.00  sec  3.61 MBytes  30.3 Mbits/sec    0    543 KBytes
[  5]  83.00-84.00  sec  4.04 MBytes  33.9 Mbits/sec    0    543 KBytes
[  5]  84.00-85.00  sec  4.35 MBytes  36.5 Mbits/sec    0    543 KBytes
[  5]  85.00-86.00  sec  3.55 MBytes  29.8 Mbits/sec    0    543 KBytes
[  5]  86.00-87.00  sec  4.17 MBytes  34.9 Mbits/sec    0    543 KBytes
[  5]  87.00-88.00  sec  4.10 MBytes  34.4 Mbits/sec    0    543 KBytes
[  5]  88.00-89.00  sec  3.49 MBytes  29.2 Mbits/sec    0    543 KBytes
[  5]  89.00-90.00  sec  3.61 MBytes  30.4 Mbits/sec    0    543 KBytes
[  5]  90.00-91.00  sec  4.04 MBytes  33.9 Mbits/sec    0    543 KBytes
[  5]  91.00-92.00  sec  4.04 MBytes  33.9 Mbits/sec    0    543 KBytes
[  5]  92.00-93.00  sec  2.88 MBytes  24.1 Mbits/sec    0    543 KBytes
[  5]  93.00-94.00  sec  3.49 MBytes  29.3 Mbits/sec    0    543 KBytes
[  5]  94.00-95.00  sec  2.82 MBytes  23.7 Mbits/sec    0    543 KBytes
[  5]  95.00-96.00  sec  3.49 MBytes  29.3 Mbits/sec    0    543 KBytes
[  5]  96.00-97.00  sec  3.49 MBytes  29.3 Mbits/sec    0    543 KBytes
[  5]  97.00-98.00  sec  4.23 MBytes  35.5 Mbits/sec    0    543 KBytes
[  5]  98.00-99.00  sec  3.92 MBytes  32.9 Mbits/sec    0    543 KBytes
[  5]  99.00-100.00 sec  3.92 MBytes  32.9 Mbits/sec    0    543 KBytes
[  5] 100.00-101.00 sec  2.82 MBytes  23.6 Mbits/sec    0    543 KBytes
[  5] 101.00-102.00 sec  3.49 MBytes  29.3 Mbits/sec    0    543 KBytes
[  5] 102.00-103.00 sec  3.00 MBytes  25.2 Mbits/sec    0    543 KBytes
[  5] 103.00-104.00 sec  3.98 MBytes  33.4 Mbits/sec    0    543 KBytes
[  5] 104.00-105.00 sec  3.43 MBytes  28.8 Mbits/sec    0    543 KBytes
[  5] 105.00-106.00 sec  4.17 MBytes  35.0 Mbits/sec    0    543 KBytes
[  5] 106.00-107.00 sec  3.49 MBytes  29.3 Mbits/sec    0    543 KBytes
[  5] 107.00-108.00 sec  3.61 MBytes  30.3 Mbits/sec    0    543 KBytes
[  5] 108.00-109.00 sec  3.55 MBytes  29.9 Mbits/sec    0    543 KBytes
[  5] 109.00-110.00 sec  3.74 MBytes  31.3 Mbits/sec    0    543 KBytes
[  5] 110.00-111.00 sec  3.55 MBytes  29.8 Mbits/sec    0    543 KBytes
[  5] 111.00-112.00 sec  4.59 MBytes  38.5 Mbits/sec    0    543 KBytes
[  5] 112.00-113.00 sec  2.94 MBytes  24.7 Mbits/sec    0    543 KBytes
[  5] 113.00-114.00 sec  2.94 MBytes  24.7 Mbits/sec    0    543 KBytes
[  5] 114.00-115.01 sec  2.94 MBytes  24.5 Mbits/sec    0    543 KBytes
[  5] 115.01-116.00 sec  4.04 MBytes  34.1 Mbits/sec    0    543 KBytes
[  5] 116.00-117.00 sec  3.68 MBytes  30.8 Mbits/sec    0    543 KBytes
[  5] 117.00-118.00 sec  4.23 MBytes  35.5 Mbits/sec    0    543 KBytes
[  5] 118.00-119.00 sec  2.94 MBytes  24.7 Mbits/sec    0    543 KBytes
[  5] 119.00-120.01 sec  3.49 MBytes  29.1 Mbits/sec    0    543 KBytes
[  5] 120.01-121.00 sec  3.55 MBytes  30.0 Mbits/sec    0    543 KBytes
[  5] 121.00-122.00 sec  4.04 MBytes  33.9 Mbits/sec    0    543 KBytes
[  5] 122.00-123.00 sec  4.23 MBytes  35.5 Mbits/sec   27    185 KBytes
[  5] 123.00-124.00 sec  3.74 MBytes  31.3 Mbits/sec   14    145 KBytes
[  5] 124.00-125.00 sec  3.49 MBytes  29.4 Mbits/sec    0    160 KBytes
[  5] 125.00-126.00 sec  2.82 MBytes  23.6 Mbits/sec    0    167 KBytes
[  5] 126.00-127.00 sec  2.88 MBytes  24.2 Mbits/sec    0    178 KBytes
[  5] 127.00-128.00 sec  3.61 MBytes  30.3 Mbits/sec    0    188 KBytes
[  5] 128.00-129.00 sec  3.37 MBytes  28.3 Mbits/sec    0    198 KBytes
[  5] 129.00-130.00 sec  3.98 MBytes  33.4 Mbits/sec    0    208 KBytes
[  5] 130.00-131.00 sec  2.94 MBytes  24.7 Mbits/sec    0    214 KBytes
[  5] 131.00-132.00 sec  2.76 MBytes  23.1 Mbits/sec    0    222 KBytes
[  5] 132.00-133.00 sec  2.94 MBytes  24.7 Mbits/sec    0    275 KBytes
[  5] 132.00-133.00 sec  2.94 MBytes  24.7 Mbits/sec    0    275 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-133.00 sec   471 MBytes  29.7 Mbits/sec  163             sender
[  5]   0.00-133.00 sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>

### AP Test

#### hostapd.conf

```
/etc/hostapd/hostapd.conf
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
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 53566
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.34 MBytes  19.6 Mbits/sec    0   68.4 KBytes
[  5]   1.00-2.00   sec  1.80 MBytes  15.1 Mbits/sec    0   68.4 KBytes
[  5]   2.00-3.00   sec  2.08 MBytes  17.5 Mbits/sec    0   68.4 KBytes
[  5]   3.00-4.00   sec  2.05 MBytes  17.2 Mbits/sec    0   68.4 KBytes
[  5]   4.00-5.00   sec  2.05 MBytes  17.2 Mbits/sec    0   68.4 KBytes
[  5]   5.00-6.00   sec  2.21 MBytes  18.5 Mbits/sec    0   68.4 KBytes
[  5]   6.00-7.00   sec  2.30 MBytes  19.3 Mbits/sec    0   68.4 KBytes
[  5]   7.00-8.00   sec  2.45 MBytes  20.6 Mbits/sec    0   68.4 KBytes
[  5]   8.00-9.00   sec  2.30 MBytes  19.3 Mbits/sec    0   68.4 KBytes
[  5]   9.00-10.00  sec  2.21 MBytes  18.5 Mbits/sec    0   68.4 KBytes
[  5]  10.00-11.00  sec  2.33 MBytes  19.5 Mbits/sec    0   68.4 KBytes
[  5]  11.00-12.00  sec  2.94 MBytes  24.7 Mbits/sec    0   68.4 KBytes
[  5]  12.00-13.00  sec  3.31 MBytes  27.7 Mbits/sec    0   68.4 KBytes
[  5]  13.00-14.00  sec  2.21 MBytes  18.5 Mbits/sec    1   68.4 KBytes
[  5]  14.00-15.00  sec  3.77 MBytes  31.6 Mbits/sec    0   68.4 KBytes
[  5]  15.00-16.00  sec  3.71 MBytes  31.1 Mbits/sec    0   68.4 KBytes
[  5]  16.00-17.00  sec  3.58 MBytes  30.1 Mbits/sec    0   68.4 KBytes
[  5]  17.00-18.00  sec  3.68 MBytes  30.8 Mbits/sec    0   68.4 KBytes
[  5]  18.00-19.00  sec  3.61 MBytes  30.3 Mbits/sec    0   68.4 KBytes
[  5]  19.00-20.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  20.00-21.00  sec  3.71 MBytes  31.1 Mbits/sec    0   68.4 KBytes
[  5]  21.00-22.00  sec  3.71 MBytes  31.1 Mbits/sec    0   68.4 KBytes
[  5]  22.00-23.00  sec  3.86 MBytes  32.4 Mbits/sec    0   68.4 KBytes
[  5]  23.00-24.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  24.00-25.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  25.00-26.00  sec  3.86 MBytes  32.4 Mbits/sec    0   68.4 KBytes
[  5]  26.00-27.00  sec  3.83 MBytes  32.1 Mbits/sec    0   68.4 KBytes
[  5]  27.00-28.00  sec  3.77 MBytes  31.6 Mbits/sec    0   68.4 KBytes
[  5]  28.00-29.00  sec  3.83 MBytes  32.1 Mbits/sec    0   68.4 KBytes
[  5]  29.00-30.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  30.00-31.00  sec  3.77 MBytes  31.6 Mbits/sec    0   68.4 KBytes
[  5]  31.00-32.00  sec  3.65 MBytes  30.6 Mbits/sec    0   68.4 KBytes
[  5]  32.00-33.00  sec  3.89 MBytes  32.6 Mbits/sec    0   68.4 KBytes
[  5]  33.00-34.00  sec  3.77 MBytes  31.6 Mbits/sec    0   68.4 KBytes
[  5]  34.00-35.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  35.00-36.00  sec  3.55 MBytes  29.8 Mbits/sec    0   68.4 KBytes
[  5]  36.00-37.00  sec  3.19 MBytes  26.7 Mbits/sec    0   68.4 KBytes
[  5]  37.00-38.00  sec  3.71 MBytes  31.1 Mbits/sec    0   68.4 KBytes
[  5]  38.00-39.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  39.00-40.00  sec  3.86 MBytes  32.4 Mbits/sec    0   68.4 KBytes
[  5]  40.00-41.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  41.00-42.00  sec  3.83 MBytes  32.1 Mbits/sec    0   68.4 KBytes
[  5]  42.00-43.00  sec  3.95 MBytes  33.1 Mbits/sec    0   68.4 KBytes
[  5]  43.00-44.00  sec  3.86 MBytes  32.4 Mbits/sec    0   68.4 KBytes
[  5]  44.00-45.00  sec  3.92 MBytes  32.9 Mbits/sec    0   68.4 KBytes
[  5]  45.00-46.00  sec  3.68 MBytes  30.8 Mbits/sec    0   68.4 KBytes
[  5]  46.00-47.00  sec  3.74 MBytes  31.3 Mbits/sec    0   68.4 KBytes
[  5]  47.00-48.00  sec  3.80 MBytes  31.9 Mbits/sec    0   68.4 KBytes
[  5]  48.00-49.00  sec  2.24 MBytes  18.8 Mbits/sec    0   68.4 KBytes
[  5]  49.00-50.00  sec   753 KBytes  6.17 Mbits/sec   22   39.9 KBytes
[  5]  49.00-50.00  sec   753 KBytes  6.17 Mbits/sec   22   39.9 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-50.00  sec   164 MBytes  27.5 Mbits/sec   23             sender
[  5]   0.00-50.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
