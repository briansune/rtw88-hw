# RTL8821CU USB Dongle Testing

### Test USB Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="../images/8821cu/rtl8821cu_arm_a35_usb.JPG" height="400"/>|<img src="../images/8821cu/rtl8821cu_usb_pcba.JPG" height="400"/>|

```
6.1.111-rt42

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

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
Flags:                                fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
```

### USB Tree

```
Before driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=, 480M

After driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=rtw_8821cu, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 003: ID 0bda:c820 Realtek Semiconductor Corp. 802.11ac NIC
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8821cu             16384  0
rtw_8821c              94208  1 rtw_8821cu
rtw_usb                24576  1 rtw_8821cu
rtw_core              217088  2 rtw_usb,rtw_8821c
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
			* 5180 MHz [36] (23.0 dBm)
			* 5200 MHz [40] (23.0 dBm)
			* 5220 MHz [44] (23.0 dBm)
			* 5240 MHz [48] (23.0 dBm)
			* 5260 MHz [52] (20.0 dBm) (radar detection)
			* 5280 MHz [56] (20.0 dBm) (radar detection)
			* 5300 MHz [60] (20.0 dBm) (radar detection)
			* 5320 MHz [64] (20.0 dBm) (radar detection)
			* 5500 MHz [100] (26.0 dBm) (radar detection)
			* 5520 MHz [104] (26.0 dBm) (radar detection)
			* 5540 MHz [108] (26.0 dBm) (radar detection)
			* 5560 MHz [112] (26.0 dBm) (radar detection)
			* 5580 MHz [116] (26.0 dBm) (radar detection)
			* 5600 MHz [120] (26.0 dBm) (radar detection)
			* 5620 MHz [124] (26.0 dBm) (radar detection)
			* 5640 MHz [128] (26.0 dBm) (radar detection)
			* 5660 MHz [132] (26.0 dBm) (radar detection)
			* 5680 MHz [136] (26.0 dBm) (radar detection)
			* 5700 MHz [140] (26.0 dBm) (radar detection)
			* 5720 MHz [144] (13.0 dBm) (radar detection)
			* 5745 MHz [149] (13.0 dBm)
			* 5765 MHz [153] (13.0 dBm)
			* 5785 MHz [157] (13.0 dBm)
			* 5805 MHz [161] (13.0 dBm)
			* 5825 MHz [165] (13.0 dBm)
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

### Network Manager - Band 2.4

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.22  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 14  bytes 2167 (2.1 KB)
        RX errors 0  dropped 1  overruns 0  frame 0
        TX packets 27  bytes 4688 (4.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.412 GHz  Access Point: 
          Bit Rate=81 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=54/70  Signal level=-56 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 29.17 Mbit/s
Testing upload speed......................................................................................................
Upload: 25.28 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=95.2 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=5.85 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=7.77 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=5.37 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=6.48 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=7.65 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=4.67 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=11.3 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=4.28 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=4.97 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=14.0 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.10 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=5.14 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=5.20 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=4.91 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=4.01 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=16.7 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=4.87 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=7.10 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=3.75 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 3.747/11.167/95.195/19.568 ms
```

#### Self-Ping 

```
PING 192.168.1.22 (192.168.1.22) 10000(10028) bytes of data.
10008 bytes from 192.168.1.22: icmp_seq=1 ttl=64 time=0.125 ms
10008 bytes from 192.168.1.22: icmp_seq=2 ttl=64 time=0.141 ms
10008 bytes from 192.168.1.22: icmp_seq=3 ttl=64 time=0.140 ms
10008 bytes from 192.168.1.22: icmp_seq=4 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.22: icmp_seq=5 ttl=64 time=0.131 ms
10008 bytes from 192.168.1.22: icmp_seq=6 ttl=64 time=0.136 ms
10008 bytes from 192.168.1.22: icmp_seq=7 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.22: icmp_seq=8 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.22: icmp_seq=9 ttl=64 time=0.141 ms
10008 bytes from 192.168.1.22: icmp_seq=10 ttl=64 time=0.132 ms
10008 bytes from 192.168.1.22: icmp_seq=11 ttl=64 time=0.110 ms
10008 bytes from 192.168.1.22: icmp_seq=12 ttl=64 time=0.107 ms
10008 bytes from 192.168.1.22: icmp_seq=13 ttl=64 time=0.127 ms
10008 bytes from 192.168.1.22: icmp_seq=14 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.22: icmp_seq=15 ttl=64 time=0.144 ms
10008 bytes from 192.168.1.22: icmp_seq=16 ttl=64 time=0.125 ms
10008 bytes from 192.168.1.22: icmp_seq=17 ttl=64 time=0.116 ms
10008 bytes from 192.168.1.22: icmp_seq=18 ttl=64 time=0.101 ms
10008 bytes from 192.168.1.22: icmp_seq=19 ttl=64 time=0.118 ms
10008 bytes from 192.168.1.22: icmp_seq=20 ttl=64 time=0.111 ms

--- 192.168.1.22 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19456ms
rtt min/avg/max/mdev = 0.101/0.125/0.145/0.014 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 53287
[  5] local 192.168.1.22 port 5201 connected to 192.168.1.3 port 53288
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  2.07 MBytes  17.3 Mbits/sec    1   68.4 KBytes       
[  5]   1.00-2.00   sec  2.02 MBytes  17.0 Mbits/sec    0   68.4 KBytes       
[  5]   2.00-3.00   sec  1.90 MBytes  15.9 Mbits/sec    1   68.4 KBytes       
[  5]   3.00-4.00   sec  2.21 MBytes  18.5 Mbits/sec    0   68.4 KBytes       
[  5]   4.00-5.00   sec  2.30 MBytes  19.3 Mbits/sec    0   68.4 KBytes       
[  5]   5.00-6.00   sec  2.27 MBytes  19.0 Mbits/sec    0   68.4 KBytes       
[  5]   6.00-7.00   sec  2.54 MBytes  21.3 Mbits/sec    1   68.4 KBytes       
[  5]   7.00-8.00   sec  2.79 MBytes  23.4 Mbits/sec    0   68.4 KBytes       
[  5]   8.00-9.00   sec  2.57 MBytes  21.6 Mbits/sec    1   68.4 KBytes       
[  5]   9.00-10.00  sec  2.63 MBytes  22.1 Mbits/sec    0   68.4 KBytes       
[  5]  10.00-11.00  sec  2.73 MBytes  22.9 Mbits/sec    0   68.4 KBytes       
[  5]  11.00-12.00  sec   502 KBytes  4.11 Mbits/sec    2   55.6 KBytes       
[  5]  12.00-13.00  sec  0.00 Bytes  0.00 bits/sec    1   54.2 KBytes       
[  5]  13.00-14.00  sec  0.00 Bytes  0.00 bits/sec    1   45.6 KBytes       
[  5]  14.00-15.00  sec   188 KBytes  1.54 Mbits/sec    0   41.3 KBytes       
[  5]  15.00-16.00  sec  0.00 Bytes  0.00 bits/sec    0   41.3 KBytes       
[  5]  16.00-17.00  sec   157 KBytes  1.29 Mbits/sec    1   32.8 KBytes       
[  5]  17.00-18.00  sec   314 KBytes  2.57 Mbits/sec    1   32.8 KBytes       
[  5]  18.00-19.00  sec  2.08 MBytes  17.5 Mbits/sec    0   62.7 KBytes       
[  5]  19.00-20.00  sec   941 KBytes  7.71 Mbits/sec    0   65.6 KBytes       
[  5]  20.00-21.00  sec   502 KBytes  4.11 Mbits/sec    1   54.2 KBytes       
[  5]  21.00-22.00  sec  1.78 MBytes  14.9 Mbits/sec    0   65.6 KBytes       
[  5]  22.00-23.00  sec  2.97 MBytes  24.9 Mbits/sec    0   65.6 KBytes       
[  5]  23.00-24.00  sec  2.45 MBytes  20.6 Mbits/sec    0   65.6 KBytes       
[  5]  24.00-25.00  sec  2.79 MBytes  23.4 Mbits/sec    0   65.6 KBytes       
[  5]  25.00-26.00  sec  2.27 MBytes  19.0 Mbits/sec    0   65.6 KBytes       
[  5]  26.00-27.00  sec  2.66 MBytes  22.4 Mbits/sec    0   65.6 KBytes       
[  5]  27.00-28.00  sec  2.27 MBytes  19.0 Mbits/sec    0   65.6 KBytes       
[  5]  28.00-29.00  sec  2.60 MBytes  21.8 Mbits/sec    0   65.6 KBytes       
[  5]  29.00-30.00  sec  2.48 MBytes  20.8 Mbits/sec    1   65.6 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.05  sec  52.9 MBytes  14.8 Mbits/sec   12             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  101.101686] rtw_core: loading out-of-tree module taints kernel.
[  101.502989] rtw_8821cu 1-1:1.2: Firmware version 24.11.0, H2C version 12
[  101.885660] usbcore: registered new interface driver rtw_8821cu
```

</details>

### Network Manager - Band 5G

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.22  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 53103  bytes 41245200 (41.2 MB)
        RX errors 0  dropped 11  overruns 0  frame 0
        TX packets 74231  bytes 94143610 (94.1 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 5G

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:5.745 GHz  Access Point: 
          Bit Rate=58.5 Mb/s   Tx-Power=13 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=39/70  Signal level=-71 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 5G

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 68.50 Mbit/s
Testing upload speed......................................................................................................
Upload: 7.54 Mbit/s
```

### Network Ping Tests - Band 5G

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=105 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=195 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=23.5 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=5.14 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=12.5 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=30.6 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=49.1 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=68.4 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=38.8 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=8.37 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=5.60 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=3.68 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=3.92 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=4.02 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=4.13 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=6.99 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=3.99 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=3.99 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=5.32 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=6.67 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19028ms
rtt min/avg/max/mdev = 3.680/29.225/195.136/46.116 ms
```

#### Self-Ping 

```
PING 192.168.1.22 (192.168.1.22) 10000(10028) bytes of data.
10008 bytes from 192.168.1.22: icmp_seq=1 ttl=64 time=0.138 ms
10008 bytes from 192.168.1.22: icmp_seq=2 ttl=64 time=0.148 ms
10008 bytes from 192.168.1.22: icmp_seq=3 ttl=64 time=0.122 ms
10008 bytes from 192.168.1.22: icmp_seq=4 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.22: icmp_seq=5 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.22: icmp_seq=6 ttl=64 time=0.106 ms
10008 bytes from 192.168.1.22: icmp_seq=7 ttl=64 time=0.149 ms
10008 bytes from 192.168.1.22: icmp_seq=8 ttl=64 time=0.156 ms
10008 bytes from 192.168.1.22: icmp_seq=9 ttl=64 time=0.116 ms
10008 bytes from 192.168.1.22: icmp_seq=10 ttl=64 time=0.100 ms
10008 bytes from 192.168.1.22: icmp_seq=11 ttl=64 time=0.119 ms
10008 bytes from 192.168.1.22: icmp_seq=12 ttl=64 time=0.125 ms
10008 bytes from 192.168.1.22: icmp_seq=13 ttl=64 time=0.150 ms
10008 bytes from 192.168.1.22: icmp_seq=14 ttl=64 time=0.153 ms
10008 bytes from 192.168.1.22: icmp_seq=15 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.22: icmp_seq=16 ttl=64 time=0.102 ms
10008 bytes from 192.168.1.22: icmp_seq=17 ttl=64 time=0.111 ms
10008 bytes from 192.168.1.22: icmp_seq=18 ttl=64 time=0.100 ms
10008 bytes from 192.168.1.22: icmp_seq=19 ttl=64 time=0.163 ms
10008 bytes from 192.168.1.22: icmp_seq=20 ttl=64 time=0.213 ms

--- 192.168.1.22 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19462ms
rtt min/avg/max/mdev = 0.100/0.131/0.213/0.028 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 52492
[  5] local 192.168.1.22 port 5201 connected to 192.168.1.3 port 52493
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   297 KBytes  2.43 Mbits/sec   28   5.70 KBytes       
[  5]   1.00-2.00   sec   502 KBytes  4.11 Mbits/sec   23   12.8 KBytes       
[  5]   2.00-3.00   sec   784 KBytes  6.42 Mbits/sec    1   32.8 KBytes       
[  5]   3.00-4.00   sec   282 KBytes  2.31 Mbits/sec   11   28.5 KBytes       
[  5]   4.00-5.00   sec   659 KBytes  5.40 Mbits/sec   17   21.4 KBytes       
[  5]   5.00-6.00   sec   659 KBytes  5.40 Mbits/sec    1   41.3 KBytes       
[  5]   6.00-7.00   sec   690 KBytes  5.65 Mbits/sec   12   41.3 KBytes       
[  5]   7.00-8.00   sec   596 KBytes  4.88 Mbits/sec    0   49.9 KBytes       
[  5]   8.00-9.00   sec   282 KBytes  2.31 Mbits/sec   23   18.5 KBytes       
[  5]   9.00-10.00  sec   502 KBytes  4.11 Mbits/sec    0   34.2 KBytes       
[  5]  10.00-11.00  sec   816 KBytes  6.68 Mbits/sec    0   49.9 KBytes       
[  5]  11.00-12.00  sec   847 KBytes  6.94 Mbits/sec    4   38.5 KBytes       
[  5]  12.00-13.00  sec  1.04 MBytes  8.74 Mbits/sec   20   20.0 KBytes       
[  5]  13.00-14.00  sec   878 KBytes  7.19 Mbits/sec    8   20.0 KBytes       
[  5]  14.00-15.00  sec   753 KBytes  6.17 Mbits/sec    0   39.9 KBytes       
[  5]  15.00-16.00  sec   878 KBytes  7.20 Mbits/sec    8   31.4 KBytes       
[  5]  16.00-17.00  sec  1.04 MBytes  8.74 Mbits/sec    0   49.9 KBytes       
[  5]  17.00-18.00  sec   941 KBytes  7.71 Mbits/sec   19   37.1 KBytes       
[  5]  18.00-19.00  sec   627 KBytes  5.14 Mbits/sec   19   31.4 KBytes       
[  5]  19.00-20.00  sec  1004 KBytes  8.22 Mbits/sec    0   79.8 KBytes       
[  5]  20.00-21.00  sec  1.16 MBytes  9.77 Mbits/sec   21   27.1 KBytes       
[  5]  21.00-22.00  sec  1004 KBytes  8.22 Mbits/sec    0   48.5 KBytes       
[  5]  22.00-23.00  sec   502 KBytes  4.11 Mbits/sec   21   28.5 KBytes       
[  5]  23.00-24.00  sec   502 KBytes  4.11 Mbits/sec   10   28.5 KBytes       
[  5]  24.00-25.00  sec   753 KBytes  6.17 Mbits/sec   16   24.2 KBytes       
[  5]  25.00-26.00  sec   502 KBytes  4.11 Mbits/sec    7   21.4 KBytes       
[  5]  26.00-27.00  sec  1004 KBytes  8.23 Mbits/sec   18   18.5 KBytes       
[  5]  27.00-28.00  sec   502 KBytes  4.11 Mbits/sec    1   25.7 KBytes       
[  5]  28.00-29.00  sec   251 KBytes  2.05 Mbits/sec    0   37.1 KBytes       
[  5]  29.00-30.00  sec   502 KBytes  4.11 Mbits/sec   13   32.8 KBytes       
[  5]  30.00-30.55  sec   251 KBytes  3.77 Mbits/sec    0   37.1 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.55  sec  20.6 MBytes  5.66 Mbits/sec  301             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  101.101686] rtw_core: loading out-of-tree module taints kernel.
[  101.502989] rtw_8821cu 1-1:1.2: Firmware version 24.11.0, H2C version 12
[  101.885660] usbcore: registered new interface driver rtw_8821cu
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
Using interface wlan0 with hwaddr and ssid "AP-NAME"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

<details>

<summary>iperf3</summary>

```
Wlan0 Not Ready.
Start AP @ WLAN0
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr bc:fd:0c:4f:23:fe and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED 
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 52516
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 52517
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  1.61 MBytes  13.5 Mbits/sec    1    147 KBytes       
[  5]   1.00-2.00   sec   314 KBytes  2.57 Mbits/sec    0    147 KBytes       
[  5]   2.00-3.00   sec   314 KBytes  2.57 Mbits/sec    0    147 KBytes       
[  5]   3.00-4.00   sec   596 KBytes  4.88 Mbits/sec    0    147 KBytes       
[  5]   4.00-5.00   sec   314 KBytes  2.57 Mbits/sec    0    147 KBytes       
[  5]   5.00-6.00   sec  0.00 Bytes  0.00 bits/sec    0    147 KBytes       
[  5]   6.00-7.00   sec   314 KBytes  2.57 Mbits/sec    0    147 KBytes       
[  5]   7.00-8.00   sec   314 KBytes  2.57 Mbits/sec    0    147 KBytes       
[  5]   8.00-9.00   sec  0.00 Bytes  0.00 bits/sec    0    147 KBytes       
[  5]   9.00-10.00  sec   314 KBytes  2.57 Mbits/sec    0    147 KBytes       
[  5]  10.00-11.00  sec   345 KBytes  2.83 Mbits/sec    0    147 KBytes       
[  5]  11.00-12.00  sec   659 KBytes  5.40 Mbits/sec    1    147 KBytes       
[  5]  12.00-13.00  sec   941 KBytes  7.71 Mbits/sec    0    147 KBytes       
[  5]  13.00-14.00  sec  1.81 MBytes  15.2 Mbits/sec    1    147 KBytes       
[  5]  14.00-15.00  sec  1.81 MBytes  15.2 Mbits/sec    0    147 KBytes       
[  5]  15.00-16.00  sec  2.42 MBytes  20.3 Mbits/sec    0    147 KBytes       
[  5]  16.00-17.00  sec  2.14 MBytes  18.0 Mbits/sec    0    147 KBytes       
[  5]  17.00-18.00  sec  2.54 MBytes  21.3 Mbits/sec    0    147 KBytes       
[  5]  18.00-19.00  sec  2.45 MBytes  20.6 Mbits/sec    0    147 KBytes       
[  5]  19.00-20.00  sec   627 KBytes  5.14 Mbits/sec    1   1.43 KBytes       
[  5]  20.00-21.00  sec  0.00 Bytes  0.00 bits/sec    1   14.3 KBytes       
[  5]  21.00-22.00  sec  0.00 Bytes  0.00 bits/sec   21    103 KBytes       
[  5]  22.00-23.00  sec  0.00 Bytes  0.00 bits/sec    0    103 KBytes       
[  5]  23.00-24.00  sec  0.00 Bytes  0.00 bits/sec    0    103 KBytes       
[  5]  24.00-25.00  sec  0.00 Bytes  0.00 bits/sec    1   61.3 KBytes       
[  5]  25.00-26.00  sec   345 KBytes  2.83 Mbits/sec    0   71.3 KBytes       
[  5]  26.00-27.00  sec  0.00 Bytes  0.00 bits/sec    1   54.2 KBytes       
[  5]  27.00-28.00  sec  0.00 Bytes  0.00 bits/sec    0   55.6 KBytes       
[  5]  28.00-29.00  sec   627 KBytes  5.14 Mbits/sec    1   45.6 KBytes       
[  5]  29.00-30.00  sec   314 KBytes  2.57 Mbits/sec    0   51.3 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.02  sec  21.0 MBytes  5.86 Mbits/sec   29             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  101.101686] rtw_core: loading out-of-tree module taints kernel.
[  101.502989] rtw_8821cu 1-1:1.2: Firmware version 24.11.0, H2C version 12
[  101.885660] usbcore: registered new interface driver rtw_8821cu
```

</details>

### End of Report
