# RTL8811CU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="../images/8811cu/rtl8811cu_arm_a9.png" height="400"/>|<img src="../images/8811cu/rtl8811cu_pcba.png" height="400"/>|

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
BogoMIPS:            799.99
Flags:               half thumb fastmult vfp edsp neon vfpv3 tls vfpd32
```

### USB Tree

```
Before driver is loaded
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=, 480M

After driver is loaded
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=rtw_8821cu, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 003: ID 0bda:c811 Realtek Semiconductor Corp.
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0 (Defined at Interface level)
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xc811
  bcdDevice            2.00
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength           53
    bNumInterfaces          1
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0xa0
      (Bus Powered)
      Remote Wakeup
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
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[   36.556558] rtw_core: loading out-of-tree module taints kernel.
[   49.315839] rtw_8821cu 1-1.1:1.0: Firmware version 24.11.0, H2C version 12
[   49.704393] usbcore: registered new interface driver rtw_8821cu

Module                  Size  Used by
rtw_8821cu             16384  0
rtw_8821c              90112  1 rtw_8821cu
rtw_usb                24576  1 rtw_8821cu
rtw_core              172032  2 rtw_usb,rtw_8821c
```

### Network Manager

```
wlan0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        RX packets 5  bytes 565 (565.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5  bytes 775 (775.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

STA is not working.

<details>

<summary>dmesg</summary>

```
[   49.315839] rtw_8821cu 1-1.1:1.0: Firmware version 24.11.0, H2C version 12
[   49.704393] usbcore: registered new interface driver rtw_8821cu
[   55.974834] random: crng init done
[   55.974847] random: 7 urandom warning(s) missed due to ratelimiting
[  962.691887] wlan0: authenticate with 
[  963.805264] wlan0: send auth to  (try 1/3)
[  963.808635] wlan0: authenticated
[  963.844921] wlan0: associate with  (try 1/3)
[  963.954831] wlan0: associate with  (try 2/3)
[  963.956170] wlan0: RX AssocResp from  (capab=0x1011 status=0 aid=3)
[  963.972295] wlan0: associated
[  964.047356] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[  967.060402] wlan0: deauthenticated from  (Reason: 15=4WAY_HANDSHAKE_TIMEOUT)
[  980.208947] wlan0: authenticate with 
[  981.625370] wlan0: send auth to  (try 1/3)
[  982.134804] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[  983.034856] wlan0: send auth to  (try 2/3)
[  983.544800] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[  983.994848] wlan0: send auth to  (try 3/3)
[  984.504801] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[  985.034820] wlan0: authentication with  timed out
[  990.552087] wlan0: authenticate with 
[  991.855288] wlan0: send auth to  (try 1/3)
[  992.364807] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[  993.034862] wlan0: send auth to  (try 2/3)
[  993.544800] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[  993.994987] wlan0: send auth to  (try 3/3)
[  994.504797] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[  995.034827] wlan0: authentication with  timed out
[  997.423425] wlan0: authenticate with 
[  998.835360] wlan0: send auth to  (try 1/3)
[  999.344809] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1000.013909] wlan0: aborting authentication with  by local choice (Reason: 3=DEAUTH_LEAVING)
[ 1022.802671] wlan0: authenticate with 
[ 1024.215282] wlan0: send auth to  (try 1/3)
[ 1024.724809] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1025.034841] wlan0: send auth to  (try 2/3)
[ 1025.544801] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1025.994841] wlan0: send auth to  (try 3/3)
[ 1026.504797] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1027.034868] wlan0: authentication with  timed out
[ 1033.375755] wlan0: authenticate with 
[ 1034.675323] wlan0: send auth to  (try 1/3)
[ 1035.184809] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1036.074852] wlan0: send auth to  (try 2/3)
[ 1036.584803] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1037.034846] wlan0: send auth to  (try 3/3)
[ 1037.544800] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1038.074832] wlan0: authentication with  timed out
[ 1110.382342] wlan0: authenticate with 
[ 1111.785333] wlan0: send auth to  (try 1/3)
[ 1112.294813] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1113.034865] wlan0: send auth to  (try 2/3)
[ 1113.544808] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1113.994996] wlan0: send auth to  (try 3/3)
[ 1114.504799] rtw_8821cu 1-1.1:1.0: failed to get tx report from firmware
[ 1115.034845] wlan0: authentication with  timed out
```

</details>

```
   Speedtest by Ookla

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
                        * 2467 MHz [12] (20.0 dBm) (no IR)
                        * 2472 MHz [13] (20.0 dBm)
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
                        * 5180 MHz [36] (20.0 dBm) (no IR)
                        * 5200 MHz [40] (20.0 dBm)
                        * 5220 MHz [44] (20.0 dBm)
                        * 5240 MHz [48] (20.0 dBm)
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
                        * 5745 MHz [149] (20.0 dBm)
                        * 5765 MHz [153] (20.0 dBm) (no IR)
                        * 5785 MHz [157] (20.0 dBm)
                        * 5805 MHz [161] (20.0 dBm)
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
```

### Server & Client Test via iperf3 (PC-Router-DUT)

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
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
wlan0: Setup of interface done.
ctrl_iface not configured
```

#### Server & Client Test via iperf3 (PC-DUT)

Although STA suffering connection troubles, AP mode shows no issue.

<details>

<summary>dmesg</summary>

```
[   45.922778] usbcore: registered new interface driver rtw_8821cu
[   52.224862] random: crng init done
[   52.224876] random: 7 urandom warning(s) missed due to ratelimiting
[   60.842292] netlink: 'hostapd': attribute type 213 has an invalid length.
[   62.055277] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[   75.945580] netlink: 'hostapd': attribute type 213 has an invalid length.
[   75.952396] netlink: 'hostapd': attribute type 213 has an invalid length.
```

</details>


<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.96, port 54934
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.96 port 54935
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.73 MBytes  22.9 Mbits/sec    0    138 KBytes
[  5]   1.00-2.00   sec  1.90 MBytes  15.9 Mbits/sec    3   65.6 KBytes
[  5]   2.00-3.00   sec  1.47 MBytes  12.3 Mbits/sec    0   65.6 KBytes
[  5]   3.00-4.00   sec  1.72 MBytes  14.4 Mbits/sec    4   49.9 KBytes
[  5]   4.00-5.00   sec  1.68 MBytes  14.1 Mbits/sec    0   65.6 KBytes
[  5]   5.00-6.00   sec  1.35 MBytes  11.3 Mbits/sec    1   65.6 KBytes
[  5]   6.00-7.00   sec  1.41 MBytes  11.8 Mbits/sec    0   65.6 KBytes
[  5]   7.00-8.00   sec  1.72 MBytes  14.4 Mbits/sec    0   65.6 KBytes
[  5]   8.00-9.00   sec  1.78 MBytes  14.9 Mbits/sec    0   65.6 KBytes
[  5]   9.00-10.00  sec  1.78 MBytes  14.9 Mbits/sec    0   65.6 KBytes
[  5]  10.00-11.00  sec  1.59 MBytes  13.4 Mbits/sec    0   65.6 KBytes
[  5]  11.00-12.00  sec  1.84 MBytes  15.4 Mbits/sec    0    115 KBytes
[  5]  12.00-13.00  sec  2.11 MBytes  17.7 Mbits/sec    2   79.8 KBytes
[  5]  13.00-14.00  sec  1.26 MBytes  10.5 Mbits/sec    0   79.8 KBytes
[  5]  14.00-15.00  sec  1.53 MBytes  12.8 Mbits/sec   33   79.8 KBytes
[  5]  15.00-16.00  sec  1.47 MBytes  12.3 Mbits/sec    0   79.8 KBytes
[  5]  16.00-17.00  sec  1.81 MBytes  15.2 Mbits/sec    0   79.8 KBytes
[  5]  17.00-18.00  sec  1.81 MBytes  15.2 Mbits/sec    0   79.8 KBytes
[  5]  18.00-19.00  sec  1.65 MBytes  13.9 Mbits/sec    0   79.8 KBytes
[  5]  19.00-20.00  sec  1.62 MBytes  13.6 Mbits/sec    2   55.6 KBytes
[  5]  20.00-21.00  sec  1.90 MBytes  15.9 Mbits/sec    1   51.3 KBytes
[  5]  21.00-22.00  sec  1.65 MBytes  13.9 Mbits/sec    0   65.6 KBytes
[  5]  22.00-23.00  sec  1.62 MBytes  13.6 Mbits/sec    0   65.6 KBytes
[  5]  23.00-24.00  sec  1.90 MBytes  15.9 Mbits/sec    0   65.6 KBytes
[  5]  24.00-25.00  sec  1.90 MBytes  15.9 Mbits/sec    6   65.6 KBytes
[  5]  25.00-26.00  sec  1.72 MBytes  14.4 Mbits/sec    0   65.6 KBytes
[  5]  26.00-27.00  sec  1.53 MBytes  12.8 Mbits/sec    0   65.6 KBytes
[  5]  27.00-28.00  sec  1.62 MBytes  13.6 Mbits/sec    4   65.6 KBytes
[  5]  28.00-29.00  sec  1.78 MBytes  14.9 Mbits/sec    0   65.6 KBytes
[  5]  29.00-30.00  sec  2.02 MBytes  17.0 Mbits/sec    0   65.6 KBytes
[  5]  30.00-31.00  sec  1.68 MBytes  14.1 Mbits/sec   28   65.6 KBytes
[  5]  31.00-32.00  sec  2.02 MBytes  17.0 Mbits/sec    3   55.6 KBytes
[  5]  32.00-33.00  sec  1.47 MBytes  12.3 Mbits/sec    1   52.8 KBytes
[  5]  33.00-34.00  sec  2.27 MBytes  19.0 Mbits/sec    0   65.6 KBytes
[  5]  34.00-35.00  sec  1.78 MBytes  14.9 Mbits/sec    1   67.0 KBytes
[  5]  35.00-36.00  sec  2.48 MBytes  20.8 Mbits/sec    0   67.0 KBytes
[  5]  36.00-37.00  sec  2.33 MBytes  19.5 Mbits/sec    1   67.0 KBytes
[  5]  37.00-38.00  sec  2.73 MBytes  22.9 Mbits/sec    0   67.0 KBytes
[  5]  38.00-39.00  sec  2.82 MBytes  23.6 Mbits/sec    0   67.0 KBytes
[  5]  39.00-40.00  sec  2.21 MBytes  18.5 Mbits/sec    0   67.0 KBytes
[  5]  40.00-41.00  sec  1.81 MBytes  15.2 Mbits/sec    0   67.0 KBytes
[  5]  41.00-42.00  sec  1.90 MBytes  15.9 Mbits/sec   10   67.0 KBytes
[  5]  42.00-43.00  sec  1.99 MBytes  16.7 Mbits/sec    0   67.0 KBytes
[  5]  43.00-44.00  sec  2.33 MBytes  19.5 Mbits/sec    1   67.0 KBytes
[  5]  44.00-45.00  sec  1.47 MBytes  12.3 Mbits/sec    2   52.8 KBytes
[  5]  45.00-46.00  sec  2.39 MBytes  20.0 Mbits/sec    0   67.0 KBytes
[  5]  46.00-47.00  sec  2.85 MBytes  23.9 Mbits/sec    1   67.0 KBytes
[  5]  47.00-48.00  sec  2.76 MBytes  23.1 Mbits/sec    0   67.0 KBytes
[  5]  48.00-49.00  sec  3.28 MBytes  27.5 Mbits/sec    0   67.0 KBytes
[  5]  49.00-50.00  sec  3.06 MBytes  25.7 Mbits/sec    0   67.0 KBytes
[  5]  50.00-51.00  sec  2.08 MBytes  17.5 Mbits/sec    0   67.0 KBytes
[  5]  51.00-52.00  sec  2.66 MBytes  22.4 Mbits/sec    0   67.0 KBytes
[  5]  52.00-53.00  sec  1.87 MBytes  15.7 Mbits/sec    1   67.0 KBytes
[  5]  53.00-54.00  sec  2.11 MBytes  17.7 Mbits/sec    3   67.0 KBytes
[  5]  54.00-55.00  sec  1.81 MBytes  15.2 Mbits/sec    0   67.0 KBytes
[  5]  55.00-56.00  sec  2.17 MBytes  18.2 Mbits/sec    0   67.0 KBytes
[  5]  56.00-57.00  sec  2.14 MBytes  18.0 Mbits/sec    0   67.0 KBytes
[  5]  57.00-58.00  sec  2.27 MBytes  19.0 Mbits/sec    0   67.0 KBytes
[  5]  58.00-59.00  sec  1.87 MBytes  15.7 Mbits/sec    1   67.0 KBytes
[  5]  59.00-60.00  sec  1.78 MBytes  14.9 Mbits/sec    0   67.0 KBytes
[  5]  60.00-61.00  sec  1.59 MBytes  13.4 Mbits/sec    0   67.0 KBytes
[  5]  61.00-62.00  sec  2.17 MBytes  18.2 Mbits/sec    0   67.0 KBytes
[  5]  62.00-63.00  sec  2.27 MBytes  19.0 Mbits/sec    0   67.0 KBytes
[  5]  63.00-64.00  sec  3.00 MBytes  25.2 Mbits/sec    0   67.0 KBytes
[  5]  64.00-65.00  sec  1.84 MBytes  15.4 Mbits/sec    0   67.0 KBytes
[  5]  65.00-66.00  sec  2.48 MBytes  20.8 Mbits/sec    0   67.0 KBytes
[  5]  66.00-67.00  sec  2.42 MBytes  20.3 Mbits/sec    8   48.5 KBytes
[  5]  67.00-68.00  sec  2.54 MBytes  21.3 Mbits/sec    2   49.9 KBytes
[  5]  68.00-69.00  sec  2.88 MBytes  24.2 Mbits/sec    1   67.0 KBytes
[  5]  69.00-70.00  sec  2.14 MBytes  18.0 Mbits/sec    0   67.0 KBytes
[  5]  70.00-71.00  sec  1.90 MBytes  15.9 Mbits/sec    0   67.0 KBytes
[  5]  71.00-72.00  sec  2.17 MBytes  18.2 Mbits/sec    8   47.1 KBytes
[  5]  72.00-73.00  sec  2.05 MBytes  17.2 Mbits/sec    0   67.0 KBytes
[  5]  73.00-74.00  sec  1.81 MBytes  15.2 Mbits/sec    0   67.0 KBytes
[  5]  74.00-75.00  sec  1.87 MBytes  15.7 Mbits/sec    4   67.0 KBytes
[  5]  75.00-76.00  sec  2.14 MBytes  18.0 Mbits/sec    0   67.0 KBytes
[  5]  76.00-77.00  sec  1.84 MBytes  15.4 Mbits/sec    0   67.0 KBytes
[  5]  77.00-78.00  sec  1.93 MBytes  16.2 Mbits/sec    0   67.0 KBytes
[  5]  78.00-79.00  sec  1.96 MBytes  16.4 Mbits/sec    0   67.0 KBytes
[  5]  79.00-80.00  sec  1.72 MBytes  14.4 Mbits/sec    0   67.0 KBytes
[  5]  80.00-81.00  sec  1.84 MBytes  15.4 Mbits/sec    0   67.0 KBytes
[  5]  81.00-82.00  sec  2.48 MBytes  20.8 Mbits/sec    0   67.0 KBytes
[  5]  82.00-83.00  sec  3.06 MBytes  25.7 Mbits/sec    0   67.0 KBytes
[  5]  83.00-84.00  sec  2.66 MBytes  22.4 Mbits/sec    0   67.0 KBytes
[  5]  84.00-85.00  sec  2.36 MBytes  19.8 Mbits/sec    0   67.0 KBytes
[  5]  85.00-86.00  sec  1.87 MBytes  15.7 Mbits/sec    0   67.0 KBytes
[  5]  86.00-87.00  sec  1.96 MBytes  16.4 Mbits/sec    0   67.0 KBytes
[  5]  86.00-87.00  sec  1.96 MBytes  16.4 Mbits/sec    0   67.0 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-87.00  sec   179 MBytes  17.2 Mbits/sec  132             sender
[  5]   0.00-87.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
