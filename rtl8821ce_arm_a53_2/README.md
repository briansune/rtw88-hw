# RTL8821CE PCIe Card Testing

### Test PCIe Gear

|Test Board|PCIe Card HW|
|-|-|
|<img src="../images/8821ce/rtl8821ce_arm_a53_2.JPG" height="400"/>|<img src="../images/8821ce/rtl8821ce_mpcie.JPG" height="400"/>|

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

### PCIe Tree

```
01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8821CE 802.11ac PCIe Wireless Network Adapter
	Subsystem: Realtek Semiconductor Co., Ltd. RTL8821CE 802.11ac PCIe Wireless Network Adapter
	Control: I/O- Mem- BusMaster- SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Interrupt: pin A routed to IRQ 255
	Region 0: I/O ports at <unassigned> [disabled]
	Region 2: Memory at e0000000 (64-bit, non-prefetchable) [disabled] [size=64K]
	Capabilities: [40] Power Management version 3
		Flags: PMEClk- DSI- D1+ D2+ AuxCurrent=375mA PME(D0+,D1+,D2+,D3hot+,D3cold+)
		Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
	Capabilities: [50] MSI: Enable- Count=1/1 Maskable- 64bit+
		Address: 0000000000000000  Data: 0000
	Capabilities: [70] Express (v2) Endpoint, MSI 00
		DevCap:	MaxPayload 128 bytes, PhantFunc 0, Latency L0s <4us, L1 <64us
			ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset- SlotPowerLimit 0.000W
		DevCtl:	Report errors: Correctable- Non-Fatal- Fatal- Unsupported-
			RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr- UncorrErr- FatalErr- UnsuppReq- AuxPwr+ TransPend-
		LnkCap:	Port #0, Speed 2.5GT/s, Width x1, ASPM L0s L1, Exit Latency L0s <512ns, L1 <64us
			ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp-
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 2.5GT/s, Width x1, TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, LTR+, OBFF Via message/WAKE#
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis-, LTR+, OBFF Disabled
		LnkCtl2: Target Link Speed: 5GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -3.5dB, EqualizationComplete-, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [100 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr+
		AERCap:	First Error Pointer: 00, GenCap+ CGenEn- ChkCap+ ChkEn-
	Capabilities: [148 v1] Device Serial Number 00-e0-4c-ff-fe-c8-21-01
	Capabilities: [158 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [160 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2+ PCI-PM_L1.1+ ASPM_L1.2+ ASPM_L1.1+ L1_PM_Substates+
			  PortCommonModeRestoreTime=30us PortTPowerOnTime=60us
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-
			   T_CommonMode=0us LTR1.2_Threshold=0ns
		L1SubCtl2: T_PwrOn=10us
	Capabilities: [170 v1] Precision Time Measurement
		PTMCap: Requester:- Responder:+ Root:-
		PTMClockGranularity: Unimplemented
		PTMControl: Enabled:- RootSelected:-
		PTMEffectiveGranularity: Unknown
	Capabilities: [17c v1] Vendor Specific Information: ID=0003 Rev=1 Len=054 <?>
	Kernel modules: rtw_8821ce

```

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8821ce             16384  0
rtw_8821c              90112  1 rtw_8821ce
rtw_pci                32768  1 rtw_8821ce
rtw_core              208896  2 rtw_8821c,rtw_pci

01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8821CE 802.11ac PCIe Wireless Network Adapter
	Subsystem: Realtek Semiconductor Co., Ltd. RTL8821CE 802.11ac PCIe Wireless Network Adapter
	Control: I/O- Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Latency: 0
	Interrupt: pin A routed to IRQ 50
	Region 0: I/O ports at <unassigned> [disabled]
	Region 2: Memory at e0000000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: [40] Power Management version 3
		Flags: PMEClk- DSI- D1+ D2+ AuxCurrent=375mA PME(D0+,D1+,D2+,D3hot+,D3cold+)
		Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
	Capabilities: [50] MSI: Enable+ Count=1/1 Maskable- 64bit+
		Address: 00000000fd480000  Data: 0000
	Capabilities: [70] Express (v2) Endpoint, MSI 00
		DevCap:	MaxPayload 128 bytes, PhantFunc 0, Latency L0s <4us, L1 <64us
			ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset- SlotPowerLimit 0.000W
		DevCtl:	Report errors: Correctable- Non-Fatal- Fatal- Unsupported-
			RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr- UncorrErr- FatalErr- UnsuppReq- AuxPwr+ TransPend-
		LnkCap:	Port #0, Speed 2.5GT/s, Width x1, ASPM L0s L1, Exit Latency L0s <512ns, L1 <64us
			ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp-
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 2.5GT/s, Width x1, TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, LTR+, OBFF Via message/WAKE#
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis+, LTR+, OBFF Disabled
		LnkCtl2: Target Link Speed: 5GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -3.5dB, EqualizationComplete-, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [100 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr+
		AERCap:	First Error Pointer: 00, GenCap+ CGenEn- ChkCap+ ChkEn-
	Capabilities: [148 v1] Device Serial Number 00-e0-4c-ff-fe-c8-21-01
	Capabilities: [158 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [160 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2+ PCI-PM_L1.1+ ASPM_L1.2+ ASPM_L1.1+ L1_PM_Substates+
			  PortCommonModeRestoreTime=30us PortTPowerOnTime=60us
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-
			   T_CommonMode=0us LTR1.2_Threshold=0ns
		L1SubCtl2: T_PwrOn=10us
	Capabilities: [170 v1] Precision Time Measurement
		PTMCap: Requester:- Responder:+ Root:-
		PTMClockGranularity: Unimplemented
		PTMControl: Enabled:- RootSelected:-
		PTMEffectiveGranularity: Unknown
	Capabilities: [17c v1] Vendor Specific Information: ID=0003 Rev=1 Len=054 <?>
	Kernel driver in use: rtw_8821ce
	Kernel modules: rtw_8821ce

[  143.387269] rtw_core: loading out-of-tree module taints kernel.
[  143.570914] rtw_8821ce 0000:01:00.0: enabling device (0000 -> 0002)
[  143.590432] rtw_8821ce 0000:01:00.0: Firmware version 24.11.0, H2C version 12
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

### Network Manager - Band 2.4

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.43  netmask 255.255.255.0  broadcast 192.168.1.255
        RX packets 28  bytes 6235 (6.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 21  bytes 3222 (3.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.427 GHz  Access Point: 
          Bit Rate=39 Mb/s   Tx-Power=30 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=70/70  Signal level=-40 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:7   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 21.13 Mbit/s
Testing upload speed......................................................................................................
Upload: 2.34 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=5.76 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=5.56 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=20.8 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=5.65 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=5.75 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=9.99 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=5.63 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=6.42 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=10.8 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=5.59 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=9.61 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=14.5 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=5.38 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=5.04 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=7.73 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=11.4 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=4.47 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=4.59 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=4.98 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=7.98 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19032ms
rtt min/avg/max/mdev = 4.471/7.893/20.810/3.986 ms
```

#### Self-Ping 

```
PING 192.168.1.43 (192.168.1.43) 10000(10028) bytes of data.
10008 bytes from 192.168.1.43: icmp_seq=1 ttl=64 time=0.104 ms
10008 bytes from 192.168.1.43: icmp_seq=2 ttl=64 time=0.066 ms
10008 bytes from 192.168.1.43: icmp_seq=3 ttl=64 time=0.071 ms
10008 bytes from 192.168.1.43: icmp_seq=4 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.43: icmp_seq=5 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=6 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=7 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=8 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.43: icmp_seq=9 ttl=64 time=0.076 ms
10008 bytes from 192.168.1.43: icmp_seq=10 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=11 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=12 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=13 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.43: icmp_seq=14 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=15 ttl=64 time=0.078 ms
10008 bytes from 192.168.1.43: icmp_seq=16 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=17 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.43: icmp_seq=18 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=19 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=20 ttl=64 time=0.072 ms

--- 192.168.1.43 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19455ms
rtt min/avg/max/mdev = 0.059/0.065/0.104/0.014 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.252, port 56033
[  5] local 192.168.1.43 port 5201 connected to 192.168.1.252 port 56034
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  1.24 MBytes  10.4 Mbits/sec    0    137 KBytes       
[  5]   1.00-2.00   sec   282 KBytes  2.31 Mbits/sec    0    137 KBytes       
[  5]   2.00-3.00   sec   282 KBytes  2.31 Mbits/sec    0    137 KBytes       
[  5]   3.00-4.00   sec   565 KBytes  4.63 Mbits/sec    0    137 KBytes       
[  5]   4.00-5.00   sec  0.00 Bytes  0.00 bits/sec    2   5.70 KBytes       
[  5]   5.00-6.00   sec  0.00 Bytes  0.00 bits/sec    3   52.8 KBytes       
[  5]   6.00-7.00   sec   282 KBytes  2.31 Mbits/sec    0   52.8 KBytes       
[  5]   7.00-8.00   sec  0.00 Bytes  0.00 bits/sec    0   52.8 KBytes       
[  5]   8.00-9.00   sec  0.00 Bytes  0.00 bits/sec    0   52.8 KBytes       
[  5]   9.00-10.00  sec  0.00 Bytes  0.00 bits/sec    0   52.8 KBytes       
[  5]  10.00-11.00  sec  0.00 Bytes  0.00 bits/sec    1   35.6 KBytes       
[  5]  11.00-12.00  sec   282 KBytes  2.31 Mbits/sec    1   28.5 KBytes       
[  5]  12.00-13.00  sec  0.00 Bytes  0.00 bits/sec    0   32.8 KBytes       
[  5]  13.00-14.00  sec  0.00 Bytes  0.00 bits/sec    6   22.8 KBytes       
[  5]  14.00-15.00  sec  0.00 Bytes  0.00 bits/sec    0   25.7 KBytes       
[  5]  15.00-16.00  sec   282 KBytes  2.31 Mbits/sec    0   29.9 KBytes       
[  5]  16.00-17.00  sec  0.00 Bytes  0.00 bits/sec    0   32.8 KBytes       
[  5]  17.00-18.00  sec   282 KBytes  2.31 Mbits/sec    0   39.9 KBytes       
[  5]  18.00-19.00  sec   282 KBytes  2.31 Mbits/sec    0   44.2 KBytes       
[  5]  19.00-20.00  sec   282 KBytes  2.31 Mbits/sec    0   49.9 KBytes       
[  5]  20.00-21.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  21.00-22.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  22.00-23.00  sec   565 KBytes  4.63 Mbits/sec    0   67.0 KBytes       
[  5]  23.00-24.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  24.00-25.00  sec   565 KBytes  4.63 Mbits/sec    0   67.0 KBytes       
[  5]  25.00-26.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  26.00-27.00  sec   565 KBytes  4.63 Mbits/sec    0   67.0 KBytes       
[  5]  27.00-28.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  28.00-29.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  29.00-30.00  sec   282 KBytes  2.31 Mbits/sec    0   67.0 KBytes       
[  5]  30.00-30.05  sec  0.00 Bytes  0.00 bits/sec    0   67.0 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.05  sec  7.58 MBytes  2.12 Mbits/sec   13             sender
[  5]   0.00-30.05  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[  143.387269] rtw_core: loading out-of-tree module taints kernel.
[  143.570914] rtw_8821ce 0000:01:00.0: enabling device (0000 -> 0002)
[  143.590432] rtw_8821ce 0000:01:00.0: Firmware version 24.11.0, H2C version 12
```

</details>

### Network Manager - Band 5G

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.43  netmask 255.255.255.0  broadcast 192.168.1.255
        RX packets 24792  bytes 30600088 (30.6 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 24616  bytes 15030209 (15.0 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 5G

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:5.24 GHz  Access Point: 
          Bit Rate=40.5 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=36/70  Signal level=-74 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:1   Missed beacon:0

```

### Network Speed Test via Ookla - Band 5G

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 50.91 Mbit/s
Testing upload speed......................................................................................................
Upload: 3.19 Mbit/s
```

### Network Ping Tests - Band 5G

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=9.04 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=9.49 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=12.1 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=10.4 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=6.20 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=6.11 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=6.14 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=15.7 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=6.98 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=11.1 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=9.60 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=4.97 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=8.87 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=4.71 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=5.36 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=5.75 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=4.47 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=8.51 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=9.95 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=6.02 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19028ms
rtt min/avg/max/mdev = 4.477/8.085/15.750/2.858 ms
```

#### Self-Ping 

```
PING 192.168.1.43 (192.168.1.43) 10000(10028) bytes of data.
10008 bytes from 192.168.1.43: icmp_seq=1 ttl=64 time=0.102 ms
10008 bytes from 192.168.1.43: icmp_seq=2 ttl=64 time=0.072 ms
10008 bytes from 192.168.1.43: icmp_seq=3 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.43: icmp_seq=4 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.43: icmp_seq=5 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.43: icmp_seq=6 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=7 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=8 ttl=64 time=0.080 ms
10008 bytes from 192.168.1.43: icmp_seq=9 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.43: icmp_seq=10 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=11 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.43: icmp_seq=12 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.43: icmp_seq=13 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.43: icmp_seq=14 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.43: icmp_seq=15 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=16 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=17 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.43: icmp_seq=18 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.43: icmp_seq=19 ttl=64 time=0.068 ms
10008 bytes from 192.168.1.43: icmp_seq=20 ttl=64 time=0.061 ms

--- 192.168.1.43 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19447ms
rtt min/avg/max/mdev = 0.059/0.065/0.102/0.011 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.252, port 56098
[  5] local 192.168.1.43 port 5201 connected to 192.168.1.252 port 56099
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  1.42 MBytes  11.9 Mbits/sec    0   89.8 KBytes       
[  5]   1.00-2.00   sec  1004 KBytes  8.22 Mbits/sec    0    107 KBytes       
[  5]   2.00-3.00   sec   502 KBytes  4.11 Mbits/sec    0    107 KBytes       
[  5]   3.00-4.00   sec   502 KBytes  4.11 Mbits/sec    0    107 KBytes       
[  5]   4.00-5.00   sec   502 KBytes  4.11 Mbits/sec    0    113 KBytes       
[  5]   5.00-6.00   sec  1.04 MBytes  8.74 Mbits/sec    0    127 KBytes       
[  5]   6.00-7.00   sec   816 KBytes  6.68 Mbits/sec    0    127 KBytes       
[  5]   7.00-8.00   sec   941 KBytes  7.71 Mbits/sec    0    127 KBytes       
[  5]   8.00-9.00   sec  1.04 MBytes  8.74 Mbits/sec    0    127 KBytes       
[  5]   9.00-10.00  sec  1.35 MBytes  11.3 Mbits/sec    0    187 KBytes       
[  5]  10.00-11.00  sec  1.10 MBytes  9.25 Mbits/sec    0    187 KBytes       
[  5]  11.00-12.00  sec  1.10 MBytes  9.25 Mbits/sec    0    187 KBytes       
[  5]  12.00-13.00  sec   753 KBytes  6.17 Mbits/sec    0    187 KBytes       
[  5]  13.00-14.00  sec  1.10 MBytes  9.25 Mbits/sec    0    187 KBytes       
[  5]  14.00-15.00  sec   753 KBytes  6.17 Mbits/sec    0    187 KBytes       
[  5]  15.00-16.00  sec  1.10 MBytes  9.25 Mbits/sec    0    187 KBytes       
[  5]  16.00-17.00  sec   753 KBytes  6.17 Mbits/sec    0    187 KBytes       
[  5]  17.00-18.00  sec  2.27 MBytes  19.0 Mbits/sec    0    187 KBytes       
[  5]  18.00-19.00  sec  3.25 MBytes  27.2 Mbits/sec    0    187 KBytes       
[  5]  19.00-20.00  sec  2.27 MBytes  19.0 Mbits/sec    0    187 KBytes       
[  5]  20.00-21.00  sec  2.70 MBytes  22.6 Mbits/sec    0    187 KBytes       
[  5]  21.00-22.00  sec  2.82 MBytes  23.6 Mbits/sec    0    187 KBytes       
[  5]  22.00-23.00  sec  2.76 MBytes  23.1 Mbits/sec    0    187 KBytes       
[  5]  23.00-24.00  sec  1.90 MBytes  15.9 Mbits/sec    0    187 KBytes       
[  5]  24.00-25.00  sec   753 KBytes  6.17 Mbits/sec    0    187 KBytes       
[  5]  25.00-26.00  sec  1.10 MBytes  9.25 Mbits/sec    0    187 KBytes       
[  5]  26.00-27.00  sec  1.10 MBytes  9.25 Mbits/sec    0    187 KBytes       
[  5]  27.00-28.00  sec  2.45 MBytes  20.6 Mbits/sec    0    187 KBytes       
[  5]  28.00-29.00  sec  1.59 MBytes  13.4 Mbits/sec    2   1.43 KBytes       
[  5]  29.00-30.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes       
[  5]  30.00-30.39  sec  0.00 Bytes  0.00 bits/sec    1    187 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.39  sec  40.6 MBytes  11.2 Mbits/sec    3             sender
[  5]   0.00-30.39  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[  143.387269] rtw_core: loading out-of-tree module taints kernel.
[  143.570914] rtw_8821ce 0000:01:00.0: enabling device (0000 -> 0002)
[  143.590432] rtw_8821ce 0000:01:00.0: Firmware version 24.11.0, H2C version 12
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
Accepted connection from 192.168.175.86, port 56137
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 56138
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.28 MBytes  19.1 Mbits/sec    0    305 KBytes       
[  5]   1.00-2.00   sec  1.29 MBytes  10.8 Mbits/sec    0    305 KBytes       
[  5]   2.00-3.00   sec  1.90 MBytes  15.9 Mbits/sec    0    305 KBytes       
[  5]   3.00-4.00   sec  1.29 MBytes  10.8 Mbits/sec    0    305 KBytes       
[  5]   4.00-5.00   sec  1.23 MBytes  10.3 Mbits/sec    0    305 KBytes       
[  5]   5.00-6.00   sec  1.96 MBytes  16.5 Mbits/sec    0    305 KBytes       
[  5]   6.00-7.00   sec  1.90 MBytes  15.9 Mbits/sec    0    305 KBytes       
[  5]   7.00-8.00   sec  3.12 MBytes  26.2 Mbits/sec    0    305 KBytes       
[  5]   8.00-9.00   sec  3.12 MBytes  26.2 Mbits/sec    0    305 KBytes       
[  5]   9.00-10.00  sec  3.12 MBytes  26.2 Mbits/sec    0    305 KBytes       
[  5]  10.00-11.00  sec  3.12 MBytes  26.2 Mbits/sec    0    305 KBytes       
[  5]  11.00-12.00  sec  3.80 MBytes  31.9 Mbits/sec    0    305 KBytes       
[  5]  12.00-13.00  sec  2.57 MBytes  21.6 Mbits/sec    0    305 KBytes       
[  5]  13.00-14.00  sec   627 KBytes  5.14 Mbits/sec    1    305 KBytes       
[  5]  14.00-15.00  sec   627 KBytes  5.14 Mbits/sec    0    305 KBytes       
[  5]  15.00-16.00  sec  0.00 Bytes  0.00 bits/sec    0    305 KBytes       
[  5]  16.00-17.00  sec   690 KBytes  5.65 Mbits/sec    0    305 KBytes       
[  5]  17.00-18.00  sec   627 KBytes  5.14 Mbits/sec    0    305 KBytes       
[  5]  18.00-19.00  sec  2.51 MBytes  21.1 Mbits/sec    0    305 KBytes       
[  5]  19.00-20.00  sec  1.23 MBytes  10.3 Mbits/sec    0    305 KBytes       
[  5]  20.00-21.00  sec  1.90 MBytes  15.9 Mbits/sec    0    305 KBytes       
[  5]  21.00-22.00  sec  0.00 Bytes  0.00 bits/sec    1    305 KBytes       
[  5]  22.00-23.00  sec   627 KBytes  5.14 Mbits/sec    0    305 KBytes       
[  5]  23.00-24.00  sec   690 KBytes  5.65 Mbits/sec    0    305 KBytes       
[  5]  24.00-25.00  sec  1.96 MBytes  16.5 Mbits/sec    0    305 KBytes       
[  5]  25.00-26.00  sec  1.29 MBytes  10.8 Mbits/sec    0    305 KBytes       
[  5]  26.00-27.00  sec  1.23 MBytes  10.3 Mbits/sec    0    305 KBytes       
[  5]  27.00-28.00  sec  1.29 MBytes  10.8 Mbits/sec    0    305 KBytes       
[  5]  28.00-29.00  sec  1.29 MBytes  10.8 Mbits/sec    0    305 KBytes       
[  5]  29.00-30.00  sec  1.23 MBytes  10.3 Mbits/sec    0    305 KBytes       
[  5]  30.00-30.04  sec  0.00 Bytes  0.00 bits/sec    0    305 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.04  sec  48.4 MBytes  13.5 Mbits/sec    2             sender
[  5]   0.00-30.04  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[  143.387269] rtw_core: loading out-of-tree module taints kernel.
[  143.570914] rtw_8821ce 0000:01:00.0: enabling device (0000 -> 0002)
[  143.590432] rtw_8821ce 0000:01:00.0: Firmware version 24.11.0, H2C version 12
```

</details>

### End of Report
