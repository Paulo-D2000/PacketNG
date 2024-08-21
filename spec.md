<center><h1> PacketNG Protocol Specification </h1></center>
<center><h1> Version 0.1 (DRAFT) </h1></center>

<h2> Introduction </h2>
This project aims to build a general Open Source Packet based transport layer for ammateur radio use employing low cost Commercial-off-the-shelf  (COTS) components. 

<h2> Project Goals </h2>

  * Reliable Digital Communication
  * Low Cost components
  * Open Source
  * TBD

<h2> Project Hardware </h2>

  * Silicon Labs Si446x RF Transceiver IC
  * RaspberryPi Foundation RP2040 Microcontroller?
  * TBD


<h2> Modulation Spec (Physical Layer) </h2>

  * 4-(G)FSK With TBD Deviation (0.5 ?)
  * *Up to 1Mbps bitrate
  * Variable Preamble Size
  * Scrambler (TBD, CCSDR 7bit or G3RUH 13bit)

<h2> Coding & Framing Spec (Data Link Layer) </h2>

  * CCSDS Concatenated Foward Error Correction Codes
      * CCSDS Convolutional Code CC(K=7, R=TDB) 
      * CCSDS Reed Solomon Code RS(255,223)
  
  * CCSDS LDPC Code ?
      * Better performance, more complex implementation, might not run on microcontrollers…
   
  * Code Rate TDB, Options are:
      * 1/2 - Most reliable transmission, lowest throughput (50 %).
      * 2/3 - TBD, higher throughput (67 %).
      * 3/4 - TBD, higher throughput (75 %)
      * 5/6 - TBD, higher throughput (83 %) [Closest ratio to DVB-S 4/5 ]
      * 7/8 - Less reliable transmission, highest throughput (88 %)
   
  *Frame Structure TBD
    [ 0 ] [ 4 Bytes ] CCSDS Syncword 1ACFFC1D
    [ 4 ] [ 4 Bytes ]  Callsign (Reverse Base36, up to 6 chars)
    [ 8 ].[ 1 Byte  ]. Data Size
    [ 8 ] [ 188 Bytes ] Data
    [ WZ  ] [ 37 43 Bytes   ] TBD (Padding ?)
    [ CRCW ] [ 4 Bytes     ] CRC-32 



  * 4 byte CCSDS Syncword 0x1ACFFC1D
