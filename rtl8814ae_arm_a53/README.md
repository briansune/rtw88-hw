# RTL8814AE PCIe Card Testing

### Test PCIe Gear

|Test Board|PCIe Card HW|
|-|-|
|<img src="../images/8814ae/rtl8814ae_arm_a53.JPG" height="400"/>|<img src="../images/8814ae/rtl8814ae_mpcie.JPG" height="400"/>|

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
01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8813AE 802.11ac PCIe Wireless Network Adapter (rev 01)
	Subsystem: Realtek Semiconductor Co., Ltd. RTL8813AE 802.11ac PCIe Wireless Network Adapter
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
		DevCap:	MaxPayload 4096 bytes, PhantFunc 1, Latency L0s <256ns, L1 <1us
			ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset- SlotPowerLimit 0.000W
		DevCtl:	Report errors: Correctable- Non-Fatal- Fatal- Unsupported-
			RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr+ UncorrErr- FatalErr+ UnsuppReq- AuxPwr+ TransPend-
		LnkCap:	Port #0, Speed 5GT/s, Width x1, ASPM L0s L1, Exit Latency L0s <4us, L1 <64us
			ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp+
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 5GT/s, Width x1, TrErr- Train- SlotClk- DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, LTR+, OBFF Via message/WAKE#
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis-, LTR-, OBFF Disabled
		LnkCtl2: Target Link Speed: 5GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete-, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [100 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr+
		AERCap:	First Error Pointer: 00, GenCap+ CGenEn- ChkCap+ ChkEn-
	Capabilities: [148 v1] Device Serial Number 00-e0-4c-ff-fe-88-13-01
	Capabilities: [158 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [160 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2+ PCI-PM_L1.1+ ASPM_L1.2+ ASPM_L1.1+ L1_PM_Substates+
			  PortCommonModeRestoreTime=150us PortTPowerOnTime=150us
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-
			   T_CommonMode=0us LTR1.2_Threshold=0ns
		L1SubCtl2: T_PwrOn=10us

```

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8814ae             16384  0
rtw_8814a             233472  1 rtw_8814ae
rtw_pci                32768  1 rtw_8814ae
rtw_core              208896  2 rtw_8814a,rtw_pci

01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8813AE 802.11ac PCIe Wireless Network Adapter (rev 01)
	Subsystem: Realtek Semiconductor Co., Ltd. RTL8813AE 802.11ac PCIe Wireless Network Adapter
	Control: I/O- Mem+ BusMaster- SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Interrupt: pin A routed to IRQ 46
	Region 0: I/O ports at <unassigned> [disabled]
	Region 2: Memory at e0000000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: [40] Power Management version 3
		Flags: PMEClk- DSI- D1+ D2+ AuxCurrent=375mA PME(D0+,D1+,D2+,D3hot+,D3cold+)
		Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
	Capabilities: [50] MSI: Enable- Count=1/1 Maskable- 64bit+
		Address: 0000000000000000  Data: 0000
	Capabilities: [70] Express (v2) Endpoint, MSI 00
		DevCap:	MaxPayload 4096 bytes, PhantFunc 1, Latency L0s <256ns, L1 <1us
			ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset- SlotPowerLimit 0.000W
		DevCtl:	Report errors: Correctable- Non-Fatal- Fatal- Unsupported-
			RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr+ UncorrErr- FatalErr+ UnsuppReq- AuxPwr+ TransPend-
		LnkCap:	Port #0, Speed 5GT/s, Width x1, ASPM L0s L1, Exit Latency L0s <4us, L1 <64us
			ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp+
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 5GT/s, Width x1, TrErr- Train- SlotClk- DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, LTR+, OBFF Via message/WAKE#
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis-, LTR-, OBFF Disabled
		LnkCtl2: Target Link Speed: 5GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete-, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [100 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr+ BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr+
		AERCap:	First Error Pointer: 00, GenCap+ CGenEn- ChkCap+ ChkEn-
	Capabilities: [148 v1] Device Serial Number 00-e0-4c-ff-fe-88-13-01
	Capabilities: [158 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [160 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2+ PCI-PM_L1.1+ ASPM_L1.2+ ASPM_L1.1+ L1_PM_Substates+
			  PortCommonModeRestoreTime=150us PortTPowerOnTime=150us
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-
			   T_CommonMode=0us LTR1.2_Threshold=0ns
		L1SubCtl2: T_PwrOn=10us

[   52.041627] rtw_core: loading out-of-tree module taints kernel.
[   52.233514] rtw_8814ae 0000:01:00.0: enabling device (0000 -> 0002)
[   52.252392] rtw_8814ae 0000:01:00.0: Firmware version 33.6.0, H2C version 6
[   52.261539] 00000000: 29 81 01 94 0d 0c 18 00 00 00 00 08 08 01 02 00  )...............
[   52.261543] 00000010: 1f 1f 1f 20 20 20 20 20 20 21 21 f3 ee ee ee ee  ...      !!.....
[   52.261547] 00000020: ee ee 24 24 24 24 24 24 24 24 24 23 23 23 23 23  ..$$$$$$$$$#####
[   52.261550] 00000030: f1 ee ee ee ee ee 20 ee ee ee 20 20 20 20 20 20  ...... ...      
[   52.261554] 00000040: 21 21 21 21 21 f2 ee ee ee ee ee ee 23 23 23 23  !!!!!.......####
[   52.261557] 00000050: 24 24 24 24 24 23 23 23 23 23 f1 ee ee ee ee ff  $$$$$#####......
[   52.261561] 00000060: 20 ee ee ee 1f 1f 1f 1e 1e 1e 20 20 1f 1e 1e f3   .........  ....
[   52.261564] 00000070: ee ee ee ee ee ee 22 22 22 22 23 23 23 23 23 23  ......""""######
[   52.261568] 00000080: 23 23 23 23 f1 ee ee ee ee ee 20 ee ee ee 1f 1f  ####...... .....
[   52.261571] 00000090: 1f 1f 1f 1f 20 20 1f 1f 1f f4 ee ee ee ee ee ee  ....  ..........
[   52.261575] 000000a0: 23 23 23 23 24 24 24 24 24 22 22 22 22 22 f1 ee  ####$$$$$"""""..
[   52.261578] 000000b0: ee ee ee ee 20 ee ee ee 7f 1f ff 00 ff ff ff ff  .... ...........
[   52.261582] 000000c0: ff 01 00 00 00 00 00 00 00 ff 00 ff ff ff ff ff  ................
[   52.261585] 000000d0: e8 4e 06 78 86 6b ec 10 13 88 ec 10 13 88 c3 ff  .N.x.k..........
[   52.261588] 000000e0: 8d 80 ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261592] 000000f0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261595] 00000100: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261599] 00000110: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261602] 00000120: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261605] 00000130: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261609] 00000140: 67 4f ff ff ff ff ff ff ff ff ff ff ff ff ff ff  gO..............
[   52.261612] 00000150: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261616] 00000160: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261619] 00000170: ff ff ff ff ff ff ff ff ff 88 f5 30 ff ff ff ff  ...........0....
[   52.261622] 00000180: ff ff 4f 16 ff ff ff ff ff ff ff ff ff ff ff ff  ..O.............
[   52.261626] 00000190: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261629] 000001a0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261633] 000001b0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261636] 000001c0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261639] 000001d0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261643] 000001e0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261646] 000001f0: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  ................
[   52.261654] rtw_8814ae 0000:01:00.0: hw cap: hci=0x00, bw=0x07, ptcl=0x03, ant_num=0, nss=3
[   52.261659] rtw_8814ae 0000:01:00.0: failed to read efuse map
[   52.267630] rtw_8814ae 0000:01:00.0: failed to setup chip efuse info
[   52.273976] rtw_8814ae 0000:01:00.0: failed to setup chip information
[   52.293025] rtw_8814ae: probe of 0000:01:00.0 failed with error -95
```

### iw list

<details>

<summary>iw list</summary>

```
```

</details>

### Network Manager - Band 2.4

```

```

### iwconfig 2.4

```
```

### Network Speed Test via Ookla - Band 2.4

```
```
