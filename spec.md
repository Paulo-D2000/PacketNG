<center><h1> PacketNG Protocol Specification </h1></center>
<center><h1> Version 0.11 (DRAFT) </h1></center>
<center><h3> Created by Paulo Dutra (PU4THZ) </h3></center>
<center><h3> Contribuitors </h3></center>
<center><h3> ... </h3></center>

<h2> Introduction </h2>
This project aims to build a general Open Source Packet based transport layer for amateur radio use employing low cost Commercial-off-the-shelf  (COTS) components. 

<h2> Project Goals </h2>

  * Reliable Digital Communication
  * Low Cost components
  * Open Source
  * TBD

<h2> Project Hardware </h2>

  * Silicon Labs Si446x RF Transceiver IC
  * Raspberry Foundation RP2040 Microcontroller?
  * TBD


<h2> Modulation Spec (Physical Layer) </h2>

  * 4-(G)FSK With TBD Deviation (0.5 ?)
  * *Up to 1 Mbps bitrate
  * Variable Preamble Size
  * Scrambler (TBD, CCSDR 7 bit or G3RUH 13 bit)

<h2> Coding & Framing Spec (Data Link Layer) </h2>

  * CCSDS Concatenated Forward Error Correction Codes
      * CCSDS Convolutional Code CC(K=7, R=TDB) 
      * CCSDS Reed Solomon Code RS(255,223)
  
  * CCSDS LDPC Code ?
      * Better performance, more complex implementation, might not run on microcontrollers…
   
  * Code Rate TDB, Options are:
      * 1/2 - Most reliable transmission, lowest throughput (50 %).
      * 2/3 - TBD, higher throughput (67 %). ?
      * 3/4 - TBD, higher throughput (75 %) ? 
      * 5/6 - TBD, higher throughput (83 %) [Closest ratio to DVB-S 4/5 ] ?
      * 7/8 - Less reliable transmission, highest throughput (88 %) ?
   
  * Frame Structure (TBD):
  
-------------------------------------------------------------------- Header Start\
    [ 0  ] [ 4 Bytes   ] CCSDS Syncword `1ACFFC1D`\
    [ 4  ] [ 4 Bytes   ] Callsign (Reverse Base 36, up to 6 chars)\
    [ 8  ] [ 1 Byte    ] Version + Flags\
    [ 9  ] [ 1 Byte    ].Payload Size\
-------------------------------------------------------------------- Header End\
    [ 10  ] [ 242 Bytes ] Payload \
    [ 252 ] [ 4 Bytes   ] CRC-32 (TBD, Might change to CRC-16)\
-------------------------------------------------------------------- Data End\

  * Version & Flags (TBD):
    * Version - [7:4] (MSB)
    * Flags   - [3:0] (LSB)
      * 4 User Flags (TBD)

<h2> Payload Spec (Application Layer) </h2>

  * Variable size user data up to 242 bytes, might include `0x00` padding (TBD).
  * Possible use case: Video Link using MPEG-TS stream. Uses only 188 bytes out of 242, padding might simplify the receiver desing, fixed size packets...
    
...
