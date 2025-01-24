# RTL8822CS SDIO PCBA Testing

### Test SDIO Gear

|Test Board|SDIO Dongle HW|
|-|-|
|<img src="../images/8822cs/rtl8723ds_arm_a53.JPG" height="400"/>|<img src="../images/8822cs/rtl8822cs_pcba.png" height="400"/>|

```
5.4.0

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.6 LTS"

Architecture:        aarch64
Byte Order:          Little Endian
CPU(s):              2
On-line CPU(s) list: 0,1
Thread(s) per core:  1
Core(s) per socket:  2
Socket(s):           1
Vendor ID:           ARM
Model:               4
Model name:          Cortex-A53
Stepping:            r0p4
CPU max MHz:         1199.9990
CPU min MHz:         299.9990
BogoMIPS:            66.66
Flags:               fp asimd aes pmull sha1 sha2 crc32 cpuid
```

### SDIO Tree

```
SDIO_CLASS=07
SDIO_ID=024C:C822
MODALIAS=sdio:c07v024CdC822
clock:		100000000 Hz
actual clock:	100000000 Hz
vdd:		21 (3.3 ~ 3.4 V)
bus mode:	2 (push-pull)
chip select:	0 (don't care)
power mode:	2 (on)
bus width:	2 (4 bits)
timing spec:	6 (sd uhs SDR104)
signal voltage:	1 (1.80 V)
driver type:	0 (driver type B)
```

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8822cs             16384  0
rtw_8822c             471040  1 rtw_8822cs
rtw_sdio               20480  1 rtw_8822cs
rtw_core              208896  2 rtw_sdio,rtw_8822c
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy1
	max # scan SSIDs: 4
	max scan IEs length: 323 bytes
	max # sched scan SSIDs: 4
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
		Capabilities: 0x19ef
			RX LDPC
			HT20/HT40
			SM Power Save disabled
			RX HT20 SGI
			RX HT40 SGI
			TX STBC
			RX STBC 1-stream
			Max AMSDU length: 7935 bytes
			DSSS/CCK HT40
		Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
		Minimum RX AMPDU time spacing: 2 usec (0x04)
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
			* 2467 MHz [12] (20.0 dBm) (no IR)
			* 2472 MHz [13] (20.0 dBm) (no IR)
			* 2484 MHz [14] (20.0 dBm) (no IR)
	Band 2:
		Capabilities: 0x19ef
			RX LDPC
			HT20/HT40
			SM Power Save disabled
			RX HT20 SGI
			RX HT40 SGI
			TX STBC
			RX STBC 1-stream
			Max AMSDU length: 7935 bytes
			DSSS/CCK HT40
		Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
		Minimum RX AMPDU time spacing: 2 usec (0x04)
		HT Max RX data rate: 300 Mbps
		HT TX/RX MCS rate indexes supported: 0-15, 32
		VHT Capabilities (0x03d071b2):
			Max MPDU length: 11454
			Supported Channel Width: neither 160 nor 80+80
			RX LDPC
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
			* 5180 MHz [36] (20.0 dBm)
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
			* 5765 MHz [153] (20.0 dBm)
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
	WoWLAN support:
		 * wake up on disconnect
		 * wake up on magic packet
		 * wake up on pattern match, up to 12 patterns of 1-128 bytes,
		   maximum packet offset 0 bytes
		 * can do GTK rekeying
		 * wake up on GTK rekey failure
		 * wake up on network detection, up to 4 match sets
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

### Network Manager - Band 2.4

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.36  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 15  bytes 2214 (2.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 18  bytes 2420 (2.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.412 GHz  Access Point: 
          Bit Rate=216 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=70/70  Signal level=-39 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 40.35 Mbit/s
Testing upload speed......................................................................................................
Upload: 3.96 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=6.70 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=3.91 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=4.05 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=6.60 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=3.68 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=7.75 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=8.44 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=3.83 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=7.72 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=4.30 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=18.4 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.29 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=5.72 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=6.38 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=4.37 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=4.48 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=3.92 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=6.16 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=10.7 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=3.78 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19029ms
rtt min/avg/max/mdev = 3.688/6.266/18.443/3.369 ms
```

#### Self-Ping 

```
PING 192.168.1.36 (192.168.1.36) 10000(10028) bytes of data.
10008 bytes from 192.168.1.36: icmp_seq=1 ttl=64 time=0.101 ms
10008 bytes from 192.168.1.36: icmp_seq=2 ttl=64 time=0.065 ms
10008 bytes from 192.168.1.36: icmp_seq=3 ttl=64 time=0.083 ms
10008 bytes from 192.168.1.36: icmp_seq=4 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=5 ttl=64 time=0.068 ms
10008 bytes from 192.168.1.36: icmp_seq=6 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.36: icmp_seq=7 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=8 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.36: icmp_seq=9 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.36: icmp_seq=10 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.36: icmp_seq=11 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=12 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.36: icmp_seq=13 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=14 ttl=64 time=0.080 ms
10008 bytes from 192.168.1.36: icmp_seq=15 ttl=64 time=0.065 ms
10008 bytes from 192.168.1.36: icmp_seq=16 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.36: icmp_seq=17 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=18 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=19 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=20 ttl=64 time=0.079 ms

--- 192.168.1.36 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19456ms
rtt min/avg/max/mdev = 0.060/0.067/0.101/0.010 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 62133
[  5] local 192.168.1.36 port 5201 connected to 192.168.1.3 port 62134
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  6.94 MBytes  58.2 Mbits/sec   23    118 KBytes       
[  5]   1.00-2.00   sec  7.54 MBytes  63.2 Mbits/sec    0    160 KBytes       
[  5]   2.00-3.00   sec  7.60 MBytes  63.7 Mbits/sec    0    191 KBytes       
[  5]   3.00-4.00   sec  7.23 MBytes  60.7 Mbits/sec    0    218 KBytes       
[  5]   4.00-5.00   sec  8.27 MBytes  69.4 Mbits/sec    0    244 KBytes       
[  5]   5.00-6.00   sec  8.82 MBytes  74.0 Mbits/sec    0    258 KBytes       
[  5]   6.00-7.00   sec  8.52 MBytes  71.4 Mbits/sec    0    258 KBytes       
[  5]   7.00-8.00   sec  8.39 MBytes  70.4 Mbits/sec    0    258 KBytes       
[  5]   8.00-9.00   sec  8.88 MBytes  74.5 Mbits/sec    0    258 KBytes       
[  5]   9.00-10.00  sec  8.27 MBytes  69.4 Mbits/sec    0    258 KBytes       
[  5]  10.00-11.00  sec  8.82 MBytes  74.0 Mbits/sec    0    258 KBytes       
[  5]  11.00-12.00  sec  8.33 MBytes  69.9 Mbits/sec    0    258 KBytes       
[  5]  12.00-13.00  sec  8.94 MBytes  75.1 Mbits/sec    0    258 KBytes       
[  5]  13.00-14.00  sec  8.45 MBytes  70.9 Mbits/sec    0    258 KBytes       
[  5]  14.00-15.00  sec  6.62 MBytes  55.5 Mbits/sec    0    258 KBytes       
[  5]  15.00-16.00  sec  4.04 MBytes  33.9 Mbits/sec    0    258 KBytes       
[  5]  16.00-17.00  sec  6.07 MBytes  50.9 Mbits/sec    0    258 KBytes       
[  5]  17.00-18.00  sec  6.07 MBytes  50.9 Mbits/sec    0    258 KBytes       
[  5]  18.00-19.00  sec  5.58 MBytes  46.8 Mbits/sec    0    258 KBytes       
[  5]  19.00-20.00  sec  5.51 MBytes  46.3 Mbits/sec    0    258 KBytes       
[  5]  20.00-21.00  sec  9.01 MBytes  75.5 Mbits/sec    0    258 KBytes       
[  5]  21.00-22.00  sec  8.52 MBytes  71.4 Mbits/sec    0    258 KBytes       
[  5]  22.00-23.00  sec  8.33 MBytes  69.9 Mbits/sec    0    258 KBytes       
[  5]  23.00-24.00  sec  8.27 MBytes  69.4 Mbits/sec    0    258 KBytes       
[  5]  24.00-25.00  sec  8.88 MBytes  74.5 Mbits/sec    0    258 KBytes       
[  5]  25.00-26.00  sec  8.82 MBytes  74.0 Mbits/sec    0    258 KBytes       
[  5]  26.00-27.00  sec  8.27 MBytes  69.4 Mbits/sec    0    258 KBytes       
[  5]  27.00-28.00  sec  8.94 MBytes  75.0 Mbits/sec    0    258 KBytes       
[  5]  28.00-29.00  sec  8.33 MBytes  69.9 Mbits/sec    0    258 KBytes       
[  5]  29.00-30.00  sec  8.88 MBytes  74.5 Mbits/sec    0    258 KBytes       
[  5]  30.00-30.03  sec   565 KBytes   135 Mbits/sec    0    258 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.03  sec   236 MBytes  65.8 Mbits/sec   23             sender
[  5]   0.00-30.03  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   23.050295] rtw_core: loading out-of-tree module taints kernel.
[   23.778562] rtw_8822cs mmc0:0001:1: WOW Firmware version 9.9.4, H2C version 15
[   23.787513] rtw_8822cs mmc0:0001:1: Firmware version 9.9.15, H2C version 15
[  122.679330] rtw_8822cs mmc0:0001:1: failed to send h2c command
[  183.360822] rtw_8822cs mmc0:0001:1: Firmware version 9.9.15, H2C version 15
[  183.360991] rtw_8822cs mmc0:0001:1: WOW Firmware version 9.9.4, H2C version 15
[  216.580080] rtw_8822cs mmc0:0001:1: failed to send h2c command
```

</details>

### Network Manager - Band 5G

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.36  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 99303  bytes 56744739 (56.7 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 191559  bytes 267282117 (267.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 5G

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:5.805 GHz  Access Point: 
          Bit Rate=390 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=58/70  Signal level=-52 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 5G

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 64.44 Mbit/s
Testing upload speed......................................................................................................
Upload: 4.02 Mbit/s
```

### Network Ping Tests - Band 5G

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=3.99 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=3.75 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.66 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=3.87 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=3.82 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=3.69 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=3.62 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=4.08 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=7.61 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=3.98 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=4.26 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.64 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=3.91 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=4.05 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=3.52 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=6.49 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=3.81 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=3.94 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=4.04 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=4.04 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19029ms
rtt min/avg/max/mdev = 3.527/4.243/7.616/0.985 ms
```

#### Self-Ping 

```
PING 192.168.1.36 (192.168.1.36) 10000(10028) bytes of data.
10008 bytes from 192.168.1.36: icmp_seq=1 ttl=64 time=0.104 ms
10008 bytes from 192.168.1.36: icmp_seq=2 ttl=64 time=0.068 ms
10008 bytes from 192.168.1.36: icmp_seq=3 ttl=64 time=0.084 ms
10008 bytes from 192.168.1.36: icmp_seq=4 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.36: icmp_seq=5 ttl=64 time=0.113 ms
10008 bytes from 192.168.1.36: icmp_seq=6 ttl=64 time=0.069 ms
10008 bytes from 192.168.1.36: icmp_seq=7 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.36: icmp_seq=8 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.36: icmp_seq=9 ttl=64 time=0.082 ms
10008 bytes from 192.168.1.36: icmp_seq=10 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.36: icmp_seq=11 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=12 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=13 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=14 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=15 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.36: icmp_seq=16 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.36: icmp_seq=17 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=18 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.36: icmp_seq=19 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.36: icmp_seq=20 ttl=64 time=0.089 ms

--- 192.168.1.36 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19451ms
rtt min/avg/max/mdev = 0.060/0.070/0.113/0.017 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 62184
[  5] local 192.168.1.36 port 5201 connected to 192.168.1.3 port 62185
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  11.3 MBytes  94.9 Mbits/sec  107    214 KBytes       
[  5]   1.00-2.00   sec  8.76 MBytes  73.5 Mbits/sec    0    242 KBytes       
[  5]   2.00-3.00   sec  9.74 MBytes  81.7 Mbits/sec    0    269 KBytes       
[  5]   3.00-4.00   sec  8.70 MBytes  73.0 Mbits/sec    0    292 KBytes       
[  5]   4.00-5.00   sec  8.88 MBytes  74.5 Mbits/sec    0    312 KBytes       
[  5]   5.00-6.00   sec  9.92 MBytes  83.3 Mbits/sec    0    327 KBytes       
[  5]   6.00-7.00   sec  8.64 MBytes  72.5 Mbits/sec    0    342 KBytes       
[  5]   7.00-8.00   sec  9.01 MBytes  75.5 Mbits/sec    0    356 KBytes       
[  5]   8.00-9.00   sec  9.80 MBytes  82.2 Mbits/sec    0    366 KBytes       
[  5]   9.00-10.00  sec  8.09 MBytes  67.8 Mbits/sec    0    379 KBytes       
[  5]  10.00-11.00  sec  8.94 MBytes  75.0 Mbits/sec    0    388 KBytes       
[  5]  11.00-12.00  sec  11.8 MBytes  99.2 Mbits/sec    0    436 KBytes       
[  5]  12.00-13.00  sec  14.7 MBytes   123 Mbits/sec    0    513 KBytes       
[  5]  13.00-14.00  sec  13.5 MBytes   114 Mbits/sec    0    513 KBytes       
[  5]  14.00-15.00  sec  14.8 MBytes   124 Mbits/sec    0    513 KBytes       
[  5]  15.00-16.00  sec  14.1 MBytes   118 Mbits/sec    0    981 KBytes       
[  5]  16.00-17.00  sec  10.0 MBytes  83.8 Mbits/sec    0    981 KBytes       
[  5]  17.00-18.00  sec  12.5 MBytes   105 Mbits/sec    0   1.19 MBytes       
[  5]  18.00-19.00  sec  15.0 MBytes   126 Mbits/sec    0   1.19 MBytes       
[  5]  19.00-20.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  20.00-21.00  sec  15.0 MBytes   126 Mbits/sec    0   1.19 MBytes       
[  5]  21.00-22.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  22.00-23.00  sec  15.0 MBytes   126 Mbits/sec    0   1.19 MBytes       
[  5]  23.00-24.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  24.00-25.00  sec  15.0 MBytes   126 Mbits/sec    0   1.19 MBytes       
[  5]  25.00-26.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  26.00-27.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  27.00-28.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  28.00-29.00  sec  13.8 MBytes   115 Mbits/sec    0   1.19 MBytes       
[  5]  29.00-30.00  sec  15.0 MBytes   126 Mbits/sec    0   1.19 MBytes       
[  5]  30.00-30.04  sec  1.25 MBytes   250 Mbits/sec    0   1.19 MBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.04  sec   366 MBytes   102 Mbits/sec  107             sender
[  5]   0.00-30.04  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   23.050295] rtw_core: loading out-of-tree module taints kernel.
[   23.778562] rtw_8822cs mmc0:0001:1: WOW Firmware version 9.9.4, H2C version 15
[   23.787513] rtw_8822cs mmc0:0001:1: Firmware version 9.9.15, H2C version 15
[  122.679330] rtw_8822cs mmc0:0001:1: failed to send h2c command
[  183.360822] rtw_8822cs mmc0:0001:1: Firmware version 9.9.15, H2C version 15
[  183.360991] rtw_8822cs mmc0:0001:1: WOW Firmware version 9.9.4, H2C version 15
[  216.580080] rtw_8822cs mmc0:0001:1: failed to send h2c command
[  388.984589] rtw_8822cs mmc0:0001:1: failed to send h2c command
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
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   23.050295] rtw_core: loading out-of-tree module taints kernel.
[   23.778562] rtw_8822cs mmc0:0001:1: WOW Firmware version 9.9.4, H2C version 15
[   23.787513] rtw_8822cs mmc0:0001:1: Firmware version 9.9.15, H2C version 15
[  122.679330] rtw_8822cs mmc0:0001:1: failed to send h2c command
[  183.360822] rtw_8822cs mmc0:0001:1: Firmware version 9.9.15, H2C version 15
[  183.360991] rtw_8822cs mmc0:0001:1: WOW Firmware version 9.9.4, H2C version 15
[  216.580080] rtw_8822cs mmc0:0001:1: failed to send h2c command
[  388.984589] rtw_8822cs mmc0:0001:1: failed to send h2c command
```

</details>

### End of Report
