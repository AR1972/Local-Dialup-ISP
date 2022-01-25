How to configure a Cisco router as a local dial up ISP, or stupid
things to do with enterprise network equipment when you are bored.

You will need a Cisco router 2821, 2851, 3825, 3845, I used a 3825.
You will also need a digital modem carrier with digital modem cards,
the modems only work with the network modules the NM-1CE1T1-PRI works,
That completes the Access Server side of the configuration. For the
dial in side you will need some FXS ports (VIC-4FXS/DID) and a
PVDM2-64 to convert analog to PCM so it can be transmitted on the 
ISDN network, also a T1 card that provides a voice-port, will be
needed, I used a VWIC2-2MFT-T1/E1. One last thing, you will need to
make a T1 PRI crossover cable to connect the VWIC2-2MFT-T1/E1 to 
the NM-1CE1T1-PRI.

https://www.kieranlane.com/2012/02/26/isdn-crossover-cable-pinout/

Once the router is assembled and configured you can connect modems to
the FXS ports and dial in with the phone number 5552221 and get on
line using the username cisco and the password cisco.

[ROUTER INVENTORY]

NAME: "3825 chassis", DESCR: "3825 chassis"
PID: CISCO3825         , VID: V03 , SN: FTX1117A17B

NAME: "VWIC2-2MFT-T1/E1 - 2-Port RJ-48 Multiflex Trunk - T1/E1 on Slot
0 SubSlot 0", DESCR: "VWIC2-2MFT-T1/E1 - 2-Port RJ-48 Multiflex Trunk -
T1/E1"
PID: VWIC2-2MFT-T1/E1  , VID: V01 , SN: FOC15200Y3D

NAME: "Four port FXS DID voice interface daughtercard on Slot 0 SubSlot
2", DESCR: "Four port FXS DID voice interface daughtercard"
PID: VIC-4FXS/DID=     , VID: 3.1, SN: FOC11245MK6

NAME: "Four port FXS DID voice interface daughtercard on Slot 0 SubSlot
3", DESCR: "Four port FXS DID voice interface daughtercard"
PID: VIC-4FXS/DID=     , VID: 3.1, SN: FOC11222QBF

NAME: "PVDMII DSP SIMM with four DSPs on Slot 0 SubSlot 4", DESCR:
"PVDMII DSP SIMM with four DSPs"
PID: PVDM2-64          , VID: V01 , SN: FOC1239666S

NAME: "Digital Modem Carrier on Slot 1", DESCR: "Digital Modem Carrier"
PID: NM-30DM=          , VID: 0.2, SN: 21947277

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164963

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164963

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165083

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165083

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164962

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164962

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165089

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165089

NAME: "One Port Channelized E1/T1/PRI with Integrated CSU on Slot 2",
DESCR: "One Port Channelized E1/T1/PRI with Integrated CSU"
PID: NM-1CE1T1-PRI=    , VID: V01 , SN: FOC11475K2A

[ROUTER CONFIG]

3825-nas-confg: enables dial in connections to use the LAN and internet

3825-bbs-confg: terminates dial in connections to a telnet server such
                 such as a BBS

as5300-confg  : config for a Cisco AS5300 allows multilink ppp via modem
                and pooing modems for various services
